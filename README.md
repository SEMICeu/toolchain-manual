# toolchain-manual

<p style="color: red; font-weight: bold">>>>>>  gd2md-html alert:  ERRORs: 0; WARNINGs: 1; ALERTS: 9.</p>
<ul style="color: red; font-weight: bold"><li>See top comment block for details on ERRORs and WARNINGs. <li>In the converted Markdown or HTML, search for inline alerts that start with >>>>>  gd2md-html alert:  for specific instances that need correction.</ul>

<p style="color: red; font-weight: bold">Links to alert messages:</p><a href="#gdcalert1">alert1</a>
<a href="#gdcalert2">alert2</a>
<a href="#gdcalert3">alert3</a>
<a href="#gdcalert4">alert4</a>
<a href="#gdcalert5">alert5</a>
<a href="#gdcalert6">alert6</a>
<a href="#gdcalert7">alert7</a>
<a href="#gdcalert8">alert8</a>
<a href="#gdcalert9">alert9</a>

<p style="color: red; font-weight: bold">>>>>> PLEASE check and correct alert issues and delete this message and the inline alerts.<hr></p>



# ​Toolchain for Publishing Data Specifications


## User Manual by SEMIC




[TOC]



# 


# Background

In the years of developing the Core Vocabularies, SEMIC has matured a lot of experience in managing the lifecycle of data specifications and their publications. After facing recurring update cycles, managing the propagation of the updates through the specifications dependencies, and orchestrating the input of multiple teams of experts into the final versions, it became clear that a systematic support would better suit the long term maintenance of the data specifications, as opposed to solely manual effort. 

SEMIC data specifications are published as HTML pages to be consulted by the experts when building their data models. More than that, SEMIC has injected the publication workflow with the ability to coherently generate models with explicit semantics. 

For the reason that every manifestation, HTML or semantic models, is sequentially processed from components that operate atomic transformation, SEMIC names this support as “Toolchain”.

The expected benefits of applying a systematic support to data specifications lifecycle are:



1. Harmonised and coherent experience of the browsing data specifications, which in turn seeks to increase the adoption
2. Promotion of SEMIC data modelling best practices, embedding them in the publication workflows
3. Support to scaling up of the editorial capacity through automation.


# Introduction

This manual describes the tooling that is supporting the editorial workflow for managing data specifications. It provides a hands-on guide on how to start reusing the SEMIC toolchain and how editors can use it to generate data specification artefacts. 

The target audience for this manual:



1. Editors operating or extending an existing SEMIC data specification;
2. Any user who wishes to customise the SEMIC publication process to create new data specifications.


# Roles, Tasks, Use Cases, Repositories and Tools 

The publication process of a data specification involves 2 roles:



* An **editor** managing the data specification within its model, metadata, layout and styling
* A **toolchain developer** in charge to setup the publication environment and processes

During the publication process, multiple tasks are performed covering different tasks executed over one or more use cases:


<table>
  <tr>
   <td><strong>Task</strong>
   </td>
   <td><strong>Use case</strong>
   </td>
  </tr>
  <tr>
   <td>Extend an existing data model
   </td>
   <td>UC1
   </td>
  </tr>
  <tr>
   <td>Updating the UML data model
   </td>
   <td>UC2
   </td>
  </tr>
  <tr>
   <td>Managing Persistent URIs
   </td>
   <td>UC3
   </td>
  </tr>
  <tr>
   <td>Editing HTML specifications
   </td>
   <td>UC4, UC5, UC6
   </td>
  </tr>
  <tr>
   <td>Deploy new software releases
   </td>
   <td>UC7
   </td>
  </tr>
  <tr>
   <td>Customise the publication process
   </td>
   <td>UC8, UC9
   </td>
  </tr>
  <tr>
   <td colspan="2" >Table 1: Publication workflow tasks and use cases
   </td>
  </tr>
</table>


The Toolchain presented in this manual relies on a set of Github repositories, and are presented in the [Table 2](#bookmark=id.ejufpwqj4w82): 


<table>
  <tr>
   <td><strong>Repository</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td><a href="https://github.com/SEMICeu/uri.semic.eu-thema">SEMIC thema</a>
   </td>
   <td>This repository mainly contains:
<ul>

<li>EAP files, to be opened by Enterprise Architect to change the data models

<li>The template folder, including templates, per language, to change the specific layout of HTML specification

<li>Site-skeleton folder, including the screenshot of each data model and the logo, to be include in the HTML specification

<li>The config folder, including the JSON configuration file per data model to change various parameters for the publication process
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><a href="https://github.com/SEMICeu/uri.semic.eu-publication">SEMIC publication</a>
   </td>
   <td>This repository mainly contains:
<ul>

<li>The template folder, including generic template that can be reused and customised by the template in the SEMIC thema repository

<li>The config folder, including the main JSON publication file under the config/dev folder 

<li>.circleci folder, including the configuration file of the CircleCI pipeline
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><a href="https://github.com/SEMICeu/uri.semic.eu-generated">SEMIC generated</a>
   </td>
   <td>This repository mainly contains:
<ul>

<li>The report folder which contains the logs of the execution of the CircleCI pipeline

<li>The doc folder, which contains the artefacts generated for each specification including the HTML specification, JSON-LD context, SHACL shapes and XSD
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><a href="https://github.com/SEMICeu/uri.semic.eu-puris">SEMIC puri</a>
   </td>
   <td>This repository mainly contains:
<ul>

<li>The release folder which contains, for each namespace, the RDF associated the respective URI
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td><a href="https://github.com/SEMICeu/uri.semic.eu-proxy">SEMIC proxy</a>
   </td>
   <td>This repository mainly contains:
<ul>

<li>The configurations for the PURI service, in particular the htmlmap.lua which perform the HTML redirection
</li>
</ul>
   </td>
  </tr>
  <tr>
   <td colspan="2" >Table 2: Toolchain Github Repositories
   </td>
  </tr>
</table>


In [Table 3](#bookmark=id.n252uta6c46t) the reader can find a summary of the repositories used, the roles involved and the tools needed per use case:


<table>
  <tr>
   <td><strong>Repositories / roles / tools</strong>
   </td>
   <td><strong>UC1</strong>
   </td>
   <td><strong>UC2</strong>
   </td>
   <td><strong>UC3</strong>
   </td>
   <td><strong>UC4</strong>
   </td>
   <td><strong>UC5</strong>
   </td>
   <td><strong>UC6</strong>
   </td>
   <td><strong>UC7</strong>
   </td>
   <td><strong>UC8</strong>
   </td>
   <td><strong>UC9</strong>
   </td>
  </tr>
  <tr>
   <td>SEMIC thema
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>SEMIC publication
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>SEMIC generated
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>SEMIC puri
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>SEMIC proxy
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Editor
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>Toolchain developer
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>Git client
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>Text editor
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>Web browser
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td>Enterprise Architect
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>HTTP client
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>SSH client
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>Linux Terminal
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>DockerHub
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>CircleCI
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td>X
   </td>
   <td>X
   </td>
   <td>X
   </td>
  </tr>
  <tr>
   <td colspan="10" >Table 3: View of Tools, Roles and Repositories needed to execute each use case
   </td>
  </tr>
</table>


As can be seen, most of the time the editor will use mainly the SEMIC thema, publication and generated repository for its operations. The editor and toolchain developer collaborate on UC3 to create and enable persistent URI’s and in UC9 to create a new SEMIC thema repository.


## 


# Tasks Execution

In order to execute the task described in this section, the reader is referred to the existing SEMIC data specification [Core Person](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic/solution/core-person-vocabulary). In this section, the first tasks in the editorial and publication process are described using mainly [Core Person](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic/solution/core-person-vocabulary) while the last tasks, covered by UC7, UC8 and UC9, focus on customising the publication process.


## Task: Extend an existing data model


### UC1: Create a new Core Person 

**Objective**

Setup a new custom data specification from an existing one in order to add new properties (UC2), create its own URI (UC3), edit metadata (UC4), update sections (UC5) and change the style of the specification (UC6). As an example in this use case, the objective is to create a copy of the existing Core Person and reuse as much as possible the current configuration.

**Roles involved**



* An editor that needs to create a new specification

**Prior Knowledge**



* How to pull, commit and push in a Git repository
* Be able to understand a JSON structure to edit configuration files

**Repositories**



* SEMIC thema repository, to access the JSON configuration file and the EAP file
* SEMIC publication repository, to access  the JSON publication file
* SEMIC generated repository, to verify the artefact generated

**Tools**



* A Git client to pull, commit and push to the repositories
* A text editor, to edit configuration files

**Steps**



1. Pull the latest code from the SEMIC thema, publication and generated repository 
2. In the SEMIC publication repository modify the publication.json file inside the config/dev folder by adding at the end the following section (just before the “]” character):

    ```
,{
    "dummy": "1",
    "urlref": "/doc/core-vocabulary/core-person-test",
    "repository": "git@uri.semic.eu-thema:SEMICeu/uri.semic.eu-thema.git",
    "branchtag": "main",
    "name": "core-person-ap",
    "filename": "config/core-person-test.json",
    "navigation": {}
  }
```



    Notice the “,” character before to concatenate with the previous section and save the file.

3. In step 2 we indicated that the filename of the JSON configuration of the new Core Person should be in the config folder of the SEMIC thema repository called core-person-test.json, so duplicate core-person-2.json and rename it core-person-test.json 
4. Edit the core-person-test.json and modify just the “eap” property to

    ```
"eap": "CorePerson-test.EAP",
```



    Be careful to keep a  “,” at the end to concatenate with the next section and save the file.

5. Now let’s duplicate CorePerson2.EAP by creating a copy named CorePerson-test.EAP
6. Commit and push in the SEMIC thema repository and after in the SEMIC publication repository.

**Test the result**

Once the publication process ended, pull the latest code from the SEMIC generated repository and verify under the doc/core-vocabulary folder, that there is a core-person-test folder (as indicated in the publication.json file) including: 



* index.html and index_en.html
* A “context” folder containing the JSON-LD context files
* A “html” folder containing the overview.jpg and semic-icon.png
* A “shacl” folder containing the SHACL shape files in turtle and JSON-LD
* A “xsd” folder containing the XML schema files


## Task: Updating the UML data model


### UC2: Adding a new property in an existing class

**Objective**

In the Core Person Test, there is a need to add “baptismal name” property within the Person class. It has been decided to:



* use the UML attribute “baptsimalName”
* use the type Text
* use the multiplicity “0..*”
* use the English label “baptismal name”
* use the English definition “the name given by Christians”
* define a new URI: http://data.europa.eu/m8g/baptismalName

**Roles involved**



* An editor that needs to add a new property in the model

**Prior Knowledge**



* How to pull, commit and push in a Git repository
* UML modelling and semantic model, see the [Data model](https://github.com/SEMICeu/documentation/blob/main/datamodel.md) section
* Be able to understand a JSON structure to edit configuration files
* Be able to understand a RDF file such as JSON-LD context and SHACL shapes

**Repositories**



* SEMIC thema repository, to access the JSON configuration file, the EAP file and site-skeleton folder
* SEMIC publication repository, to access  the JSON publication file
* SEMIC generated repository, to verify the artefact generated

**Tools**



* A Git client to pull, commit and push to the repositories
* Enterprise Architect to apply changes to the UML class diagram
* A text editor, to edit configuration file and to test that the generated artefacts (JSON-LD context and SHACL shapes) have been updated correctly
* A web browser, to test that the generated HTML specification has been updated correctly

**Steps**



1. Pull the latest code from the SEMIC thema repository 
2. Open the CorePerson-test.EAP file with Enterprise Architect
3. In “Project Browser” ribbon, expand the Core Person package, double click on the diagram called “Core_Person_publication”, select the class Person
4. In the “Feature & Properties” ribbon add new attribute with Name “baptsimalName”
5. Next define the Type “Text” to be selected from the drop-down menu “Select Type…” under “Core Vocabulary” package
6. Select the Scope “Public”

    

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")


7. In the “Attribute Properties” ribbon, look for the Multiplicity property and select the default value “[1]”, double click on it and select Lower bound to 0 and Upper bound *, click OK

    

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")


8. In the “Tagged Values” ribbon, select the now empty “Attribute (baptsimalName)” section, click on “Add new tagged value” icon, in Tag type “label-en” with Value “baptismal name”, click OK

    

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")


9. Click again on “Add new tagged value” icon, in Tag type “definition-en” with Value “the name given by Christians”, click OK
10. Click again on “Add new tagged value” icon, in Tag type “uri” with Value “http://data.europa.eu/m8g/baptismalName”, click OK
11. As the UML diagram changed but we reuse the same folder of the original Core Person, we change the core-person-test.json file and modify just the “site” property to

    ```
"site": "site-skeleton/core-person-test",
```



    and save the file.

12. Under “site-skeleton” folder duplicate the core-person folder and rename it “core-person-test 
13. From Enterprise Architect, save the picture of the UML diagram from the menu “Publish -> Image -> Save to File” and save it under the “site-skeleton/core-person-test” folder with the name “overview.jpg”, overwriting the current one.
14. Commit the 4 files changed (CorePerson-test.EAP, core-person-test.json and overview.jpg and semic-icon.png) and push to them to the SEMIC thema repository
15. Update the publication.json file in the SEMIC publication repository by changing the dummy value to

    ```
"dummy": "2",
```



    and commit and push to the SEMIC publication repository


**Test the result**

Once the publication process ended, pull the latest code from the SEMIC generated repository and verify under the doc/core-vocabulary folder, that there is a core-person-test folder including:



* The image “overview.jpg”, located in the html folder and linked from the index.html, has been updated including the new property
* The new property appears under the Person class section in the index.html file, with the respective label, definition and multiplicity

    

<p id="gdcalert4" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image4.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert5">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image4.png "image_tooltip")


* The new property appears in the generated artefacts JSON-LD context, SHACL shapes, etc.)


## Task: Managing Persistent URIs


### UC3: Create a persistent URI for a new property

**Objective**

Having created the new property “baptismal name” in use case UC2, there is a need to create a new persistent URI related to the property.

When a specification is officially released, the persistent URI is maintained as RDF redirection and HTML redirection, both will be setup in this use case.

**Roles involved**



* An editor that needs to define a new persistent URI
* A toolchain developer to enable the new persistent URI

**Prior Knowledge**



* How to pull, commit and push in a Git repository
* Having read the [Persistent URI documentation](https://github.com/SEMICeu/documentation/blob/main/puri.md)
* For RDF redirection:
    * Be able to understand a RDF file in the formats Turtle, RDF/XML or N-Triples
* For HTML redirection:
    * Having setup the HTML specification release; in the case of SEMIC, the index.html generated in UC2 is assumed to be published on [https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/](https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/) thanks to GitHub Pages
* To enable Persistent URI service:
    * Understand how to connect to a remote machine via SSH
    * Basic knowledge of Linux command line
    * Having setup a personal access token on its own GitHub profile that allows to pull code of GitHub via command line
* To test, basic knowledge of HTTP protocol in order to set the Accept header

**Tools**



* A Git client to pull, commit and push to the repositories
* A SSH key pair setup within to PURI service machine and a SSH Client
* A text editor, to edit RDF files and configuration file
* For the RDF redirection, a HTTP client that allows to send a Accept Header 
* For the HTML redirection, a browser that can display the HTML response

**Steps**



1. To setup the RDF redirection, pull the latest code from the SEMIC puri repository
    1. Under releases/m8g folder, create 3 empty files: baptsimalName.nt, baptsimalName.rdf and baptsimalName.ttl
    2. Open with a text editor the baptsimalName.ttl and type the following:

        ```
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<http://data.europa.eu/m8g/baptsimalName>
    a rdf:Property, <http://www.w3.org/2002/07/owl#DatatypeProperty> ;
     <http://www.w3.org/2000/01/rdf-schema#isDefinedBy>  
<http://data.europa.eu/m8g> ;
    <http://www.w3.org/2004/02/skos/core#scopeNote> "the name given by Christians."@en ;
  <http://www.w3.org/2000/01/rdf-schema#label> "baptsimal name"@en .
```



    And save the file.

    3. For the other 2 formats, either they are typed manually or they can be generated with automatic tools such as [EasyRDF](https://www.easyrdf.org/converter), [RDF translator](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwiwwrnOtvb7AhUN2xoKHVyPCh0QFnoECBEQAQ&url=https%3A%2F%2Frdf-translator.appspot.com%2F&usg=AOvVaw1My-fDwxW5-ZC29xHa5JQy), [RDF validator](http://rdfvalidator.mybluemix.net/)… 
    4. Commit and push the changes in the SEMIC puri repository
2. To setup the HTML redirection, pull the latest code from the SEMIC proxy repository
    5. Open, with a text editor, the file “htmlmap.lua” and add, at the end of the file (before the “}”  character), a line for for the new URI:

        ```
["/m8g/baptismalName"] = "https://semiceu.github.io/Core-Person-Vocabulary/releases/2.00/#Person%3Abaptismal%20name"
```



    and save the file.


    Be careful to add a “,” character at the end of the previous line so the properties can be correctly read.


    Notice the last part of the line “Person%3Abaptismal%20name”, this is the HTML id generated in the UC2 in the index.html concatenating the class with property name.

    6. Commit and push the changes to the SEMIC proxy repository
3. The toolchain developer will enable the persistent URI by entering the Persistence Service machine via SSH client and perform the following commands:

<table>
  <tr>
   <td>
<strong>Command</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>cd uri.semic.eu-proxy/
   </td>
   <td>Enter in the folder of the SEMIC proxy repository
   </td>
  </tr>
  <tr>
   <td>git pull
   </td>
   <td>Insert the GitHub username and personal access token
   </td>
  </tr>
  <tr>
   <td>make nginx 
   </td>
   <td>Create a new version of the nginx web server
   </td>
  </tr>
  <tr>
   <td>make run<em> </em>
   </td>
   <td>Run the nginx web server
   </td>
  </tr>
</table>


**Test the result**



* For the RDF redirection, open the HTTP client and create a HTTP request pointing to [http://data.europa.eu/m8g/baptsimalName](http://data.europa.eu/m8g/baptsimalName):
    * by setting the Accept header to “text/turtle”, it should get an answer like in step 1.2
    * by setting the Accept header to “rdf/xml”, it should get an answer in RDF/XML as saved in step 1.3
    * By setting the Accept header to “application/n-triples”, it should get an answer in N-Triples as saved in step 1.3



<p id="gdcalert5" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image5.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert6">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image5.png "image_tooltip")




* For the HTML redirection, open the browser or the HTTP client and point to the URL [http://data.europa.eu/m8g/baptsimalName](http://data.europa.eu/m8g/baptsimalName), it should get redirected to the URL specified in step 2.1, pointing to the exact HTML section of the property


## Task: Editing HTML specifications


### UC4: Update the publication metadata of the specification

**Objective**

There is a need to update the metadata of the specification; in order to create a draft for this new release, the following properties are going to be updated:



* Publication state, to be set to “SEMIC Draft”
* Publication date, to be set to “2023-01-01”

**Roles involved**



* An editor that needs to update the specification

**Prior Knowledge**



* How to pull, commit and push in a Git repository
* Be able to understand a JSON structure to edit configuration files

**Repositories**



* SEMIC thema repository, to access the JSON configuration file
* SEMIC publication repository, to access  the JSON publication file
* SEMIC generated repository, to verify the artefact generated

**Tools**



* A Git client to pull, commit and push to the repositories
* A text editor, to edit configuration file
* To test, a web browser that can display the HTML specification

**Steps**



1. Pull the latest code from the SEMIC thema repository
2. Open with a text editor the core-person-test.json under the config property
3. Change the respective lines:

    ```
"publication-state": "Semic Draft",
"publication-date": "2023-01-01",
```



    Be careful to add a “,” character after each line and save the file.

4. Commit and push the file changed in the SEMIC thema repository
5. Pull the latest code from the SEMIC publication repository
6. Update the publication.json file in the SEMIC publication repository by changing the dummy value to

    ```
"dummy": "3",
```



    and commit and push to the SEMIC publication repository


**Test the result**

Once the publication process ends, pull the latest code from the SEMIC generated repository and verify under the doc/core-vocabulary folder, that there is a core-person-test folder including the index.html file.

Open the index.html with a browser and verify that the 2 properties have been correctly updated.



<p id="gdcalert6" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image6.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert7">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image6.png "image_tooltip")



### UC5: Adding a changelog section in the specification

**Objective**

Having created a new property in UC2, there is a need to inform readers of the new specification about what has been changed via a change log. The change log will be a  custom section in the specification.

**Roles involved**



* An editor that needs to update the specification with a changelog

**Prior Knowledge**



* How to pull, commit and push in a Git repository
* Be able to understand a JSON structure to edit configuration files
* Be able to understand the template structure  

**Repositories**



* SEMIC thema repository, to access the JSON configuration and the template files
* SEMIC publication repository, to access the JSON publication file
* SEMIC generated repository, to verify the artefact generated

**Tools**



* A Git client to pull, commit and push to the repositories
* A text editor, to edit configuration files
* To test, a web browser that can display the HTML specification

**Steps**



7. Pull the latest code from the SEMIC thema repository
8. Open with a text editor the core-person-test.json under the config property
9. Change the following line:

    ```
 "template": "core-person-ap-test_en.j2",
```



    Be careful to add a “,” character at the end of the line and save the file.

10. Now go in the “template” folders and duplicate the core-person-ap_en.j2 file into core-person-ap-test_en.j2
11. Open the core-person-ap-test_en.j2 and change the change log section with the following text and save the file:

    ```
{% block changelog %}
<p>
The new property "baptsimal name" has been added.
<p>
{% endblock %}
```



    Notice the {% block changelog %} at the beginning and the {% endblock %} at the end to enclose the changelog block that will be used by a generic template.

12. Commit and push the files changed in the SEMIC thema repository
13. Pull the latest code from the SEMIC publication repository
14. Update the publication.json file in the SEMIC publication repository by changing the dummy value to

    ```
"dummy": "4",
```



    and commit and push to the SEMIC publication repository


**Test the result**

Once the publication process ends, pull the latest code from the SEMIC generated repository and verify under the doc/core-vocabulary folder, that there is a core-person-test folder including the index.html file.

Open the index.html with a browser and verify that the section change log has been correctly updated.



<p id="gdcalert7" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image7.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert8">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image7.png "image_tooltip")



### UC6: Changing the colour of the hyperlinks

**Objective**

In order to reflect the style of the organisation creating the new specification, the HTML specification can be changed by changing the colour of the hyperlinks to the green colour.

**Roles involved**



* An editor that needs to customise the style of the specification

**Prior Knowledge**



* How to pull, commit and push in a Git repository
* Be able to understand a JSON structure to edit configuration files
* Be able to understand the template structure  
* Knowledge of HTML/CSS to be applied to the new template 

**Repositories**



* SEMIC publication repository, to change the local template
* SEMIC publication repository, to create a generic template and access to the JSON publication file
* SEMIC generated repository, to verify the artefact generated

**Tools**



* A Git client to pull, commit and push to the repositories
* A text editor, to edit configuration files
* To test, a web browser that can display the HTML specification

**Steps**



1. Pull the latest code from the SEMIC thema repository
2. Open the core-person-ap-test_en.j2 in the “template” folder, change the extends header to the following and save the file:

    ```
{% extends "semic_core_voc_test.j2" %}
```




<p id="gdcalert8" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: Definition &darr;&darr; outside of definition list. Missing preceding term(s)? </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert9">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


:



3. Commit and push the files changed in the SEMIC thema repository
4. Pull the latest code from the SEMIC publication repository
5. Go under the “templates” folder and duplicate the generic template semic_core_voc.j2 file to semic_core_voc_test.j2 file.
6. Open the semic_core_voc_test.js file with a text editor and add, towards the end, the following lines: 

    ```
a, a:hover {
   color: #00cc23;
}
```



    Just before the  &lt;/style> tag.

7. Update the publication.json file in the SEMIC publication repository by changing the dummy value to

    ```
"dummy": "5",
```



    and commit and push to the SEMIC publication repository


**Test the result**

Once the publication process ends, pull the latest code from the SEMIC generated repository and verify under the doc/core-vocabulary folder, that there is a core-person-test folder including the index.html file.

Open the index.html with a browser and verify that the colour of the hyperlinks has been correctly updated.



<p id="gdcalert9" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image8.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert10">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image8.png "image_tooltip")



## Task: Deploy new software releases


### UC7: Activate a new release of transformation software in the toolchain

**Objective**

The toolchain is based upon open source software which are distributed as Docker images.

As software evolves new versions of the software will become available. Each new version will result in a release of a new Docker image with a new version number. 

Within this use case, the objective is to change the toolchain so that it will use a new software release. We will upgrade the software that extracts the information from the UML model.

(NOTE) How software is being developed, maintained and released is the responsibility of the software component itself. Each (open source) software component will have its own methodology, approach and lifecycle.   

**Roles involved**



* A toolchain developer that wants to update the toolchain to the new release of the transformation software.

**Prior Knowledge**



* How to build and run Docker container images
* Being able to read Docker container images specification (i.e. Dockerfile), and in particular understand how Docker images are interconnected with each other
* Knowledge about CI/CD and in particular of CircleCI (https://circleci.com/docs/)
* A GitHub account that is connected with SEMIC publication repository and which is also registered as a CircleCI user
* A DockerHub account ([https://hub.docker.com](https://hub.docker.com)) for exploring the latest version releases
* Be familiar with the YAML notation

**Repositories**



* SEMIC publication repository, to access  the CircleCI configuration file
* SEMIC generated repository, to verify removal of the generated examples

**Tools**



* A Git client to pull, commit and push to the repositories
* An text editor, to edit the CircleCI configuration
* A web browser to access CircleCI web interface (https://circleci.com) 
* Docker Hub ([https://hub.docker.com/](https://hub.docker.com/)) as image repository distributing the toolchain Docker images 

**Steps**



1. Pull the latest code from the SEMIC publication repository
2. Open with the text editor the CircleCI configuration (file .circleci/config.yml)
3. Find the image declaration of the software that is to be upgraded : [https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/.circleci/config.yml#L115](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/.circleci/config.yml#L115)
4. Login into DockerHub and search for the image informatievlaanderen/oslo-ea-to-rdf
5. Find the tag that corresponds with the to-be deployed release, i.e. [json-ld-format-m1.1.3](https://hub.docker.com/layers/informatievlaanderen/oslo-ea-to-rdf/json-ld-format-m1.1.3/images/sha256-4f860f868acc64ddc94da9943cfca78240d15b4911ff9ef5bac835ab5876639e?context=repo)
6. Change in the Docker image tag at line 115 in the CircleCI configuration file to the selected release
7. Commit and push the change to the SEMIC publication repository

**Test the result**

In the CircleCI web interface one can see the execution of the toolchain. If the Docker image was found by CircleCI, and the new release of the software had no breaking (API) changes compared to the previous version, the execution will be successful and the output visible in the SEMIC generated repository. 

Otherwise the execution will halt at the step with an error. Resolving errors can happen in numerous ways: 



* by inspecting the logs in the CircleCI web interface;
* by rerunning the failed step via the CircleCI web interface with an temporary ssh connection and debugging the situation on a real execution state;
* Reverting back to the original software by resetting the Docker image tag to the original value.

(NOTE) Despite it may be needed to resolve an issue for one data specification, updating software releases is a global change for the toolchain. It impacts all current and future creations of data specifications specified in the SEMIC publication repository. Therefore such changes should be communicated to all editors.


## Task: Customise the publication process


### UC8: Using CircleCI to build data specifications

**Objective**

To automate building data specifications, the toolchain is using the CI/CD solution CircleCI. 

Consider the case that the generation of examples is not required for data specifications. Therefore, the objective is to adapt the CircleCI workflow to reflect that decision and exclude the generation of examples.

**Roles involved**



* A toolchain developer that wants to update the workflow of the toolchain

**Prior Knowledge**



* Knowledge about CI/CD and in particular of [CircleCI](https://circleci.com/docs/)
* A GitHub account that is connected with SEMIC publication repository and which is also registered as a CircleCI user
* Familiarity with the YAML notation

**Repositories**



* SEMIC publication repository, to access the CircleCI configuration file
* SEMIC generated repository, to verify removal of the generated examples

**Tools**



* A Git client to pull, commit and push to the repositories
* A text editor to edit configuration files
* A web browser to access [CircleCI web interface](https://circleci.com)

**Steps**

Part 1 - enable examples being generated for a specification



1. Pull the latest code from the SEMIC publication repository 
2. Select in the SEMIC generated repository a data specification to create examples for. Let's consider this specification: Core Person test.
3. Trigger the build process for the selected data specification by updating the publication.json file in the SEMIC publication repository by setting the configuration property “examples” to “true”

    ```
"examples": "true",
```



    Commit and push to the SEMIC publication repository

4. Verify in the SEMIC generated repository that the examples are created (see https://github.com/SEMICeu/uri.semic.eu-generated/tree/master/examples/core-person-test)
5. In the web interface of CircleCI the latest execution trace should mention a step in the visualised workflow called “render-example-templates”.

      


Part 2 - adapt the workflow to not generate the examples.



6. Open with the text editor the CircleCI configuration (file .circleci/config.yml) within the SEMIC publication repository
7. Outcomment the lines 566-568 ([https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/.circleci/config.yml#L566](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/.circleci/config.yml#L566)) by putting a # symbol as the first character of each line
8. Outcomment line 601 (#- `render-example-templates)`
9. Commit and push the change to the SEMIC publication repository
10. Select in the SEMIC generated repository a data specification that has NO examples yet
11. Trigger the build process for an existing specification by updating the publication.json file in the SEMIC publication repository by changing the dummy value to

    ```
"dummy": "6",
```



    and commit and push to the SEMIC publication repository


**Test the result**

Once the last change has happened the CircleCI will not anymore create examples, even when the property in the publication JSON is present. This is because the code that would react to this property (being true or false) is not anymore executed. This code has become dormant in the updated CircleCI configuration.

To verify the effect of the change, select another data specification that has no examples present and apply the steps of part 1 for that specification.One will observe that no examples are being created in the SEMIC generated repository. 

One also can see the change in the CircleCI web interface. By outcommenting the lines the step has become dormant and is not anymore visible in the workflow. 


### UC9: Initiating a new SEMIC thema repository

**Objective**

In use cases 1 - 6, the current setup of the SEMIC toolchain is assumed: a single thema repository containing all Core Vocabularies. However, not all SEMIC data specifications follow the same life cycle as the Core Vocabularies, for instance DCAT-AP. In that case it is recommended to manage the data specification in its own thema repository.

This use case will initiate a new thema repository for a data specification. 

**Roles involved**



* An editor that needs to create a new data specification
* A toolchain developer that needs to initiate the new thema repository for that new data specification

**Prior Knowledge **



* GitHub account with all necessary permissions
* How to pull, commit and push in a Git repository
* How to work with GitHub templates
* Be able to understand a JSON structure to edit configuration files
* Knowledge about the data specification (naming, etc.)

**Repositories**



* SEMIC publication repository, to initiate an initial build
* SEMIC generated repository, to verify the transformation outcome

**Tools**



* A Git client to pull, commit and push to the repositories
* An text editor, to edit configurations files
* A web browser to access [CircleCI web interface](https://circleci.com)

**Steps**

Part 1 - Initialise a new thema repository with boilerplate information 



1. The toolchain developer will login into GitHub using its web browser 
2. Then select thema template on GitHub ([https://github.com/Informatievlaanderen/OSLOthema-template](https://github.com/Informatievlaanderen/OSLOthema-template)) 
3. Use the template to create in the target organisation space a new GitHub repository. In this case, the organisation is SEMICeu and the repository name will be Semicthema-DCAT-AP. This will result in the new GitHub repository https://github.com/SEMICeu/Semicthema-DCAT-AP. Note that the visibility of the new repository is a policy decision; the toolchain is capable of handling public and as well private repositories
4. Enable the access rights for the editors according to the organisation's policy
5. As the template contains dummy, placeholder files, the new thema repository is ready to be used

Part 2 - Initialise the new thema repository with concrete information of the new data specification



1. Configure with the editor the new data specification content in the repository
    1. Adapt the config file that describes the data specification and change the file name to reflect the data specification that is configured in that file
    2. Adapt the UML file to hold an initial version of the data specification
    3. Adapt the stakeholders file to describe all initial collaborators to the data specification
    4. Adapt the overview image to hold the initial version of the data specification
    5. Adapt the template files to hold the initial summary and supportive texts 
2. Clean up and remove any non used boilerplate information
3. Document all these changes in the CHANGELOG file (in the root of the thema repository) and commit and push the changes

Part 3 - Trigger a build of the data specification in SEMIC publication repository

These steps are similar to the explanation in UC1, and are thus summarised here in short.



1. Pull the latest code from the SEMIC publication repository
2. In the SEMIC publication repository modify the publication.json file inside the config/dev folder by adding at the end the following section (just before the “]” character):

    ```
,{
    "dummy": "1",
    "urlref": "/doc/applicationprofile/DCAT-AP",
    "repository": "git@uri.semic.eu-thema:SEMICeu/Semicthema-DCAT-AP.git",
    "branchtag": "main",
    "name": "dcat-ap",
    "filename": "config/dcat-ap.json",
    "navigation": {}
  }
```



        This defines a new publication based on the content of the newly created thema  repository



1. Commit and push the change to the SEMIC publication repository 

**Test the result**

When the new thema repository is correctly configured then the last step will result in an update to the SEMIC generated repository. A new directory will appear: /doc/applicationprofile/DCAT-AP.

In case of errors, consult the CircleCI web interface to find the step that caused the error. The most frequent sources of problems are: 



* The JSON configuration files are not in the proper JSON syntax. In this case, a JSON formatter can be used (e.g., [jq](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwj5tpDpt_b7AhVhgc4BHTWBBXIQFnoECA8QAQ&url=https%3A%2F%2Fjqplay.org%2F&usg=AOvVaw32nsoMdEDWyJ_cAtdjZ0oz&cshid=1670929115779122), [JSON formatter and validator](https://jsonformatter.curiousconcept.com/)…)
* The configuration values refer to non-existing information like a non-existing diagram in the UML file, a non-existing template, etc.
* Usage of  special characters and whitespace characters may also be a source of problems,  but these are usually part of the data specification content. While these are the editors responsibility, the toolchain developer might be involved to find the exact source of these.