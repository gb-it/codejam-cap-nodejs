# Exercise 02

In this exercise you'll become familiar with the workflow of creating a new CAP project from the command line, and discover how quickly you can get to a basic OData service serving a simple metadata document.

One of the challenges of building a full stack app using OData has been the production of an OData service - the definition of the metadata and the creation of the backend components to service the OData operations.

With Core Data & Services (CDS) as the definition language and CAP as the framework providing out-of-the-box services that respond to OData requests, that challenge has disappeared. It's very easy to get a basic OData service up and running in only a few minutes. Being able to rapidly get to a working metadata document has various benefits which we'll discuss at the end of this exercise.

## Covering (partially from [notes](../orgdocs/notes.md))

- Difference between db and srv (data model and service)
- Getting a basic OData service (at least the metadata) up quickly, without even any persistence layer (`cds run`) (basic = a single entity, no relationships or anything, probably based on the sample Books from `cds init`)
- Small excursion into OData, showing service document, metadata document, and data resources
- Exploring what we have in the basic project (folders, files)

## Steps

After completing these steps you'll be familiar with how you can use the CDS commandline tool to initialize a project with an OData service.

### Initialize a new CAP project

The first thing to do in any new CAP based project is to initialize that project by indirectly creating a directory with various basic files in it. This can be achieved with the CDS commandline tool `cds` which you installed in [exercise 01](../01/).

The `cds` tool should be available in your executable path, having been installed as part of the Node.js `@sap/cds` package in the [previous exercise](../01/).

:point_right: First, explore the `cds` commandline tool by executing it with no parameters; you will see what options are available:

```sh
user@host:~
=> cds

USAGE

    cds <command> [<args>]


COMMANDS

  c | compile    ...individual models (= the default)
  d | deploy     ...data models to a database
  s | serve      ...service models to REST clients
  b | build      ...whole modules or projects
  i | init       ...jump-starts a new project
  e | env        get/set current cds configuration
  r | repl       cds's read-eval-event-loop
  h | help       shows usage for cds and individual commands
  v | version    prints detailed version information

  cds help <command> gives more help about each (also with --help)
  cds <file> without <command> defaults to cds compile.
  cds without any arguments shows this help.


EXAMPLES

  cds model.cds
  cds compile model.cds
  cds compile model.json --to cdl
  cds serve cat-service
  cds build --clean
  cds compile --help
```

Note that with `cds init` a new project can be quickly initialized.

:point_right: Explore what options are available with `cds init` with the `--help` option:

```sh
user@host:~
=> cds init --help
```

Amongst other things, you should see a `--modules` option to specify a list of modules to be created when the project is initialized, and also a `--verbose` option.

:point_right: Use both of these options to initialize a new project directory thus:

```sh
user@host:~
=> cds init --modules db, srv --verbose bookshop
```

You should see output that looks similar to this:

```sh
Creating new project in directory bookshop.

Copying templates for type db to bookshop/db ...
Copying templates for type srv to bookshop/srv ...
Updating npm dependencies in bookshop/package.json ...
Running npm install...
npm WARN bookshop@1.0.0 license should be a valid SPDX license expression

added 76 packages from 109 contributors and audited 166 packages in 3.261s
found 0 vulnerabilities


Project creation was successful.
```

### Open the project in VS Code

Now that the project has been initialized, it's time to explore it. The VS Code IDE is a comfortable environment in which to do so, so at this point you will open up the newly created `bookshop` directory in it.

:point_right: Open up the new `bookshop` directory in VS Code. One way to do this (if the installation of VS Code on your operating system put the binary in your executable path) is simply by invoking `code` on the command line, and specifying the directory to open:

```sh
user@host:~
=> code bookshop
```

If this approach is not available to you, simply start VS Code through your operating system's GUI and open the directory manually.

### Explore the initialized project structure

The skeleton project that has been initialized is visible in VS Code. This is what it should look like (it shows also the `db/data-model.cds` file opened, which you can do manually):

![initialized project in VS Code](initialized-project-in-vscode.png)

:point_right: Examine what files have been populated in the project directory structure.

Briefly, the directories and contents can be described thus:

| Directory      | Contents |
| -------------- | -------- |
| `.vscode`      | VS Code specific files for launch configurations (useful for debugging) |
| `db`           | Where the data models (in CDS) are specified. A skeleton CDS project that has been initialized with the `--modules db` option will have a basic data model file in the form of `data-model.cds` with a small sample definition, like here |
| `node_modules` | This is the normal place where NPM packages (modules) are to be found in a Node.js based project |
| `srv`          | Where the service definitions (in CDS) are specified. A skeleton CDS project that has been initialized with the `--modules srv` option will have a basic service definition file in the form of `cat-service.cds` with a small service definition, like here |

Besides the directories there are also a number of files, including the project's `package.json` (present in any Node.js based project and a readme file.


## Summary

## Questions

Why is there an focus on "TTM" (time to metadata) - what advantages does that bring?
What is the difference between the data model and the service definition? Why do we need both?
