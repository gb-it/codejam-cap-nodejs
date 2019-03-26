# Exercise 08 - Introducing an app at the UI layer

In this exercise you'll add a UI layer, by adding annotations that can drive aspects of a user interface (UI), and introducing a Fiori Elements based app.


## Steps

Following these steps, you'll build a simple Fiori app that sits in a local Fiori launchpad environment, and that serves up book details from the `CatalogService` OData service, helped by annotations that you'll be specifying.


### 1. Introduce a basic HTML page to be served for the UI

Following the "convention over configuation" theme, the Node.js flavored CAP will also automatically serve static resources (such as UI artefacts) from a directory called `app/`. If there isn't an `app/` directory it will serve the "Welcome to cds.services" landing page we've seen already:

![the "Welcome to cds.services" landing page](../07/two-services.png)

If there is an `app/` directory with content, it will serve that instead.

:point_right: Create an `app/` directory, at the same level as the `db/` and `srv` directories, and create an `index.html` file within it, containing the following:

```html
<!DOCTYPE html>
<html>
<head>

	<meta http-equiv="X-UA-Compatible" content="IE=edge" />
	<meta http-equiv="Content-Type" content="text/html;charset=UTF-8" />
	<title>Bookshop</title>


</head>
<body class="sapUiBody" id="content"></body>
</html>
```

:point_right: Restart the service (with `cds serve all`) and go to the root URL, i.e. [http://localhost:4004](http://localhost:4004). This time, you are not shown the "Welcome to cds.services" landing page - instead, the page is empty, except for the page title in the browser tab, that shows us that the HTML we entered has been loaded:

![title in browser tab](title-in-browser-tab.png)


### 2. Add a Fiori sandbox environment to the UI index page

To create a sandbox Fiori launchpad we'll need the UI5 runtime as well as artefacts from the `test-resources` area of the toolkit.

:point_right: Add these three `script` tags between the `title` element and the end of the `head` element:

```html
    <script
        src="https://sapui5.hana.ondemand.com/1.63.1/test-resources/sap/ushell/bootstrap/sandbox.js"></script>

    <script id="sap-ui-bootstrap"
        src="https://sapui5.hana.ondemand.com/1.63.1/resources/sap-ui-core.js"
        data-sap-ui-libs="sap.m,sap.ushell,sap.collaboration,sap.ui.layout"
        data-sap-ui-compatVersion="edge"
        data-sap-ui-theme="sap_belize"
        data-sap-ui-frameOptions="allow"></script>

    <script>
        sap.ui.getCore().attachInit(function() {
            sap.ushell.Container.createRenderer("fiori2").placeAt("content")
        })
    </script>
```

Reloading the browser tab should now show the beginnings of something recognizable as a Fiori launchpad:

![an empty Fiori launchpad](empty-fiori-launchpad.png)

Great!


### 3. Introduce a basic UI app to the Fiori launchpad

Now we have the launchpad as a container for our app, let's introduce it gradually.

:point_right: First, add an entry to the sandbox launchpad configuration to define a tile and the app to which it should be connected, by adding this `applications` property (for a "Browse Books" app) to the "sap-ushell-config" in the `index.html` file (the surrounding context is shown for clarity):

```javascript
window["sap-ushell-config"] = {
	defaultRenderer: "fiori2",
	applications: {
		"browse-books": {
			title: "Browse Books",
			description: "Bookshop",
			additionalInformation: "SAPUI5.Component=bookshop",
			applicationType : "URL",
			url: "/browse/webapp"
		}
	}
};
```

Reloading the index page in the browser should show this:

![Fiori launchpad with tile](launchpad-with-tile.png)


## Summary

...


## Questions

...



