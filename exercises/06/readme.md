# Exercise 06

In this exercise you'll enhance the service definition with annotations, and introduce a second service that sits on top of the same underlying data model.


- Basic annotations (@readonly, @insertonly) in the service
- Introducing a second service on the same data model (admin related)


## Steps

At the end of these steps, you'll have two OData services both exposing different views on the same underlying data model.


### 1. Import a collection of HTTP requests into Postman

:point_right: In the same way that you did in [exercise 05](../05/), import a collection of HTTP requests into your Postman client via the URL to [postman-06.json](TODO.json).

This contains a number of different requests ready for you to try.

TODO - screenshot of entire collection

### 2. Test the existing write access to Books and Authors

Right now the `Books` and `Authors` entities are exposed in the `CatalogService` service. In the subsequent steps in this exercise we'll be tightening the restrictions down to read-only. Before we do, let's check to see that, at least currently, we have write access. We'll do that by making a couple of OData Create operations, one to create a new author, and the other to add a book by that author.

:point_right: In the Postman collection you imported, try out the requests in the folder "**(A) Before @readonly annotations**", running them in the order they're presented (the creation of the new book is for the new author, which needs to exist first).

Note that the creation requests are successful, and you can see the new author and book in an OData Query operation: [http://localhost:4004/catalog/Authors?$expand=books](http://localhost:4004/catalog/Authors?$expand=books).


### 3. Restrict access to the Books and Authors entities

Now, we want to only allow read-only operations on the master data. This can be achieved with OData annotations that are encapsulated into a convenient `@readonly` [shortcut](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/227cbf1a3ec24075a3aaaf6202f88be5.html).

:point_right: Add this to each of the `Books` and `Authors` specifications in the `CatalogService` thus:

```cds
service CatalogService {
    @readonly entity Books as projection on my.Books;
    @readonly entity Authors as projection on my.Authors;
    entity Orders as projection on my.Orders;
}
```

What does this do, precisely?

:point_right: First save the file then redeploy & restart the service, like you did in [exercise 05](../05/):

```sh
user@host:~/bookshop
=> cds deploy && cds serve all
```

:point_right: Now examine the OData service's [metadata](http://localhost:4004/catalog/$metadata), and you should find annotations that look like this:

![readonly annotations](readonly-annotations.png)

Is this just a recommendation that can be overridden? Let's find out.















## Summary



## Questions

What are the advantages to separating the data model and service layers? Are there any disadvantages?

