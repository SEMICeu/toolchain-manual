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