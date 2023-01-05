# ​Toolchain for Publishing Data Specifications -  User Manual by SEMIC

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

| Task                                                                  | Use cases     |
|-----------------------------------------------------------------------|---------------|
| [Extend an existing data model](extend_existing_data_model.md)        | UC1           |
| [Updating the UML data model](updating_UML_data_model.md)             | UC2           | 
| [Managing Persistent URIs](managing_persistent_URIs.md)               | UC3           |
| [Editing HTML specifications](editing_HTML_specifications.md)         | UC4, UC5, UC6 |
| [Deploy new software releases](deploy_new_software_releases.md)       | UC7           |
| [Customise the publication process](customise_publication_process.md) | UC8, UC9      |


The Toolchain presented in this manual relies on a set of Github repositories, and are presented in the below table: 

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
</table>


In the below table the reader can find a summary of the repositories used, the roles involved and the tools needed per use case:


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
   <td><strong>Roles</strong>
   </td>
   <td colspan="9">
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
