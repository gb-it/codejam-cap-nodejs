# Exercise 03

In this exercise you'll enhance your basic bookshop project by adding to the data model and service definition, and creating a persistence layer.

## Covering (partially from [notes](../orgdocs/notes.md))

- Adding a new Authors entity definition
- Looking at relationships between Authors and Books and how we describe them in CDS
- Establishing a persistence layer (cds deploy)
- Understanding what's going on underneath (cds compile)
- Seeding the persistence layer and service with data via CSV
- Introducing more entities and building relationships between them (Associations / Compositions)
- Trying out OData operations (CRUD+Q) on the basic service


## Steps

After completing these steps you'll have a slightly more complex OData service, with a second entity that is related to the first.


### Add a new Authors entity to the model

Currently the data model is extremely simple. In this step you'll add a second entity 'Authors'.

:point_right: Open the `db/data-model.cds` file in VS Code and add a new entity definition, after the `Books` entity, thus:

```cds
entity Authors {
  key ID : Integer;
  name   : String;
}
```

This is deliberately very simple at this point. Don't forget to save the file.

:point_right: In the integrated terminal, start (or restart) the service like this:

```sh
user@host:~/bookshop
=> cds serve all
```

(If you want, you can also use `cds serve srv` like you did in [exercise 02](../02/)).

:point_right: Open up (or refresh) the [service metadata document](http://localhost:4004/catalog/$metadata) and check for the entity definition you've just added.

You're right. It's not there.


### Expose the Authors entity in the service

While there is now a second entity definition in the data model, it is not exposed in the existing service. In this step, you'll remedy that.

:point_right: Open up the `srv/cat-service.cds` file and add a second entity to the `CatalogService` definition. While you're there, remove the `@readonly` annotation that you see against the existing entity in the service - we will look at these annotations in a later exercise. This is what the contents of `srv/cat-service.cds` should look like after you've added the new entity and removed the annotation:

```cds
using my.bookshop as my from '../db/data-model';

service CatalogService {
    entity Books as projection on my.Books;
    entity Authors as projection on my.Authors;
}
```

:point_right: Restart the service and check the metadata document once again. The definition of the Authors entity should now be present in the metadata, and will look something like this:

![Books and Authors entities in the metadata document](books-authors-metadata-document.png)

This is nice, but there's something fundamental that's missing.


### Add a relationship between the Books and Authors entities.

The Books and Authors entities are standalone and currently are not related to each other. This is not ideal, so in this step you'll fix that by adding a relationship in the form of an [association](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/9ead8e4701d04848a6fdc84356723a52.html).

:point_right: Return to the `db/data-model.cds` file and add an association from the Books entity to the Authors entity, bearing in mind the simplified assumption that a book has a single author. The association should describe a new `author` property in the Books entity like this:

```cds
entity Books {
  key ID : Integer;
  title  : String;
  stock  : Integer;
  author : Assocation to Authors;
}
```

Note that as you type, the CDS Language Services extension that you installed in [exercise 01](../01/) provides very useful command completion, recognising the entities defined as well as the CDS syntax itself:

![command completion](command-completion.png)

This `Association to Authors` relationship will allow a consumer to navigate from a Book to the related Author, but not from an Author to their Books. Let's fix that now by adding a second association.

:point_right: To the Authors entity, add a `books` property thus:

```cds
entity Authors {
  key ID : Integer;
  name   : String;
  books  : Association to many Books on books.author = $self;
}
```

Note that this is a 'to-many' relationship. Don't forget to save the file.

:point_right: Restart the service and check the metadata document again. There should now be OData navigation properties defined between the two entities, like this:

![navigation properties](navigation-properties.png)

## Summary



## Questions

Why does placing CSV files in a certain place just work? (convention ove configuration philosophy)
What happens to the content of `package.json` after a deploy?
What are some of the differences between OData V2 and V4 with respect to query options?

