# Exercise 02

In this exercise you'll become familiar with the workflow of creating a new CAP project from the command line, and discover how quickly you can get to a basic OData service serving a simple metadata document.

One of the challenges of building a full stack app using OData has been the production of an OData service - the definition of the metadata and the creation of the backend components to service the OData operations.

With Core Data & Services (CDS) as the definition language and CAP as the framework providing out-of-the-box services that respond to OData requests, that challenge has disappeared. It's very easy to get a basic OData service up and running in only a few minutes. Being able to rapidly get to a working metadata document has various benefits which we'll discuss at the end of this exercise.

## Covering (partially from [notes](../orgdocs/notes.md))

- Looking at different options of `cds init`
- Difference between db and srv (data model and service)
- Getting a basic OData service (at least the metadata) up quickly, without even any persistence layer (`cds run`) (basic = a single entity, no relationships or anything, probably based on the sample Books from `cds init`)
- Small excursion into OData, showing service document, metadata document, and data resources
- Exploring what we have in the basic project (folders, files)

## Steps

After completing these steps you'll be familiar with how you can use the CDS commandline tool to initialize a project with an OData service.

### Initialize a new CAP project

The first thing to do in any new CAP based project is to initialize that project by indirectly creating a directory with various basic files in it. This can be achieved with the CDS commandline tool `cap` which you installed in [exercise 01](../01/).

## Summary

## Questions

Why is there an focus on "TTM" (time to metadata) - what advantages does that bring?
What is the difference between the data model and the service definition? Why do we need both?
