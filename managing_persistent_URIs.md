#### [<<< Previous page:  Task-Updating the UML data model ](updating_UML_data_model.md) --- [Next page: Task-Editing HTML specifications >>>](editing_HTML_specifications.md)

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
   <td><strong>Command</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>cd uri.semic.eu-proxy/</td>
   <td>Enter in the folder of the SEMIC proxy repository</td>
  </tr>
  <tr>
   <td>git pull</td>
   <td>Insert the GitHub username and personal access token</td>
  </tr>
  <tr>
   <td>make nginx</td>
   <td>Create a new version of the nginx web server</td>
  </tr>
  <tr>
   <td>make run</td>
   <td>Run the nginx web server</td>
  </tr>
</table>

**Test the result**

* For the RDF redirection, open the HTTP client and create a HTTP request pointing to [http://data.europa.eu/m8g/baptsimalName](http://data.europa.eu/m8g/baptsimalName):
    * by setting the Accept header to “text/turtle”, it should get an answer like in step 1.2
    * by setting the Accept header to “rdf/xml”, it should get an answer in RDF/XML as saved in step 1.3
    * By setting the Accept header to “application/n-triples”, it should get an answer in N-Triples as saved in step 1.3

![alt_text](images/image5.png "image_tooltip")

* For the HTML redirection, open the browser or the HTTP client and point to the URL [http://data.europa.eu/m8g/baptsimalName](http://data.europa.eu/m8g/baptsimalName), it should get redirected to the URL specified in step 2.1, pointing to the exact HTML section of the property

#### [<<< Previous page:  Task-Updating the UML data model ](updating_UML_data_model.md) --- [Next page: Task-Editing HTML specifications >>>](editing_HTML_specifications.md)