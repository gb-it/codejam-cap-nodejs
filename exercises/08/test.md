# Exercise 08 - Introducing an app at the UI layer

Test


## Steps

Test


### Introduce a basic HTML page to be served for the UI


### Add a Fiori sandbox environment to the UI index page



### Introduce a basic UI app to the Fiori launchpad


Reloading the index page in the browser should show this:

![Fiori launchpad with tile](launchpad-with-tile.png)



### Bring in the main part of the app

:point_right: Create a file `index.cds` in the `app/` directory, and add the following content:

```cds
using from './browse/fiori-service';
using my.bookshop as my from '../db/data-model';

// Authors Elements
annotate my.Authors with {
    ID @title:'{i18n>ID}' @UI.HiddenFilter;
    name @title:'{i18n>AuthorName}';
}
```


### Create the app directory and the app-specific CDS file

## Summary

## Questions
