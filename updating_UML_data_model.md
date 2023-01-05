#### [<<< Previous page: Task-Extend an existing model ](extend_existing_data_model.md) --- [Next page: Task-Managing Persistent URIs >>>](managing_persistent_URIs.md)

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

	![alt_text](images/image1.png "Adding attribute")

7. In the “Attribute Properties” ribbon, look for the Multiplicity property and select the default value “[1]”, double click on it and select Lower bound to 0 and Upper bound *, click OK

	![alt_text](images/image2.png "Set the multiplicity")

8. In the “Tagged Values” ribbon, select the now empty “Attribute (baptsimalName)” section, click on “Add new tagged value” icon, in Tag type “label-en” with Value “baptismal name”, click OK

	![alt_text](images/image3.png "Set the label")

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

	![alt_text](images/image4.png "Verify attribute is present in HTML page")

* The new property appears in the generated artefacts JSON-LD context, SHACL shapes, etc.

#### [<<< Previous page: Task-Extend an existing model ](extend_existing_data_model.md) --- [Next page: Task-Managing Persistent URIs >>>](managing_persistent_URIs.md)