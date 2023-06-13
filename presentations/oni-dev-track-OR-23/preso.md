---
title: Introducing the Oni Repository Stack 
author:
- Peter Sefton
- Moises Sacal Bonequi
- Alvin Sebastian
- Mark Raadgever
theme:
- Copenhagen
date:
- 2023-06-12

---





# The architecture

![](oni_diagrams_oni-architecture-2.svg)

::: notes


### Abstract

In this presentation we will show some of the general purpose repository tooling used to manage repository data for the Language Data Commons of Australia and the Australian Text Analytics Platform. We have a standards-based repository stack which is used to make research data available for human and machine-use. The main part of the stack is “Oni” https://github.com/Arkisto-Platform/oni which builds an access-controlled REST API from an Oxford Common File Layout (OCFL) data store (which consists of data objects which are saved as files-on-disk or in object storage), with data objects are described using the RO-Crate metadata standard. Data is indexed into a postgres-driven API for low-level access, and a full discovery index implemented in ElasticSearch, with the ability to create access portals in your web framework of choice. We will demonstrate rapid creation of large scale repositories using batch tooling, as well as using a metadata entry tool known as Describo to produce RO-Crate linked-data descriptions.


This slide shows the "small pieces, loosely joined style of the Oni repository" -- it is based on an OCFL data store for digital objects on disk or object storage - with RO-Crate metadata for each object.
:::

# Some data – ~300 plays from the 1500s

![](list-metadata.gif)

::: notes
Very often researchers will have 

:::
# Using RO-Crate-excel, execute a few maneuvers

![](rocxl.mov.gif)

::: notes
In this recording, we use the RO-Crate Excel tool to generate an Excel workbook listing all the files.

:::

# Paste in the researcher's data

![](sheet-detail.png)

# Fine tune using Crate-O ...

![](crate-o-org.mov.gif)

::: notes

Here we see the Crate-O metadata tool (which is a zero-install web application that runs in Chrome and other browsers that support the new FilesystemAPI) being used to add an Orgnization as the Affiliation for a Person entity. Having imported this "Context Entity" (that's the RO-Crate term for this type of contextual metadata) it can then be re-used within the crate which we see here as the schema.org `publisher` property is linked to the same orgnization.
:::



# Here's where you get Crate-O

![](crate-o-site.png)

::: notes

You can get the Crate-O source or try it out [at this github repo](https://github.com/Language-Research-Technology/crate-o).

:::

# … and you get an RO-Crate for the data

![](rochtml.mov.gif)

::: notes
This slide shows generating an HTML preview file that summarizes the data

:::

# Then using corpus-tools-ro-crate, make an OCFL repo

![](make-plays.mov.gif)

::: notes
This slide shows another script (via a make file that supplies a set of commandline paramaters) which takes the RO-Crate and "explodes" it into a set of OCFL (Oxford Common File Layout) directories in a "Storage Root" 

:::

# This is the OCFL file layout

![](ocfl-screenshot.png)

# Start up 👹 and index stuff

Type, like:

```
> docker compose up

 ... Screenfulls of stuff

> node structural-index.js 

{ message: 'Started: database indexer' }



```


# Et Voila!

![](portal.mov.gif)

::: notes

This is a search portal for the plays with an Elastic search for full text for ~~facets~~ aggregations.

In conclusion, this repository stack is quite different from DSpace, ePrints and other repository systems where everything is built in to one application - the approach is more like the unix 

:::


# Tools used here

This presentation: https://github.com/Language-Research-Technology/qa/tree/main/presentations/oni-dev-track-OR-23

The excel-to-crate tooling: https://github.com/Language-Research-Technology/ro-crate-excel

The thing that turns RO-Crate into an OCFL repo: https://github.com/Language-Research-Technology/corpus-tools-ro-crate

The Oni stack, OCFL library, API and Elastic Search: https://github.com/Language-Research-Technology/oni-ui





