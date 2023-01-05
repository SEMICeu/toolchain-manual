#### [<<< Previous page: Task-Deploy new software releases ](deploy_new_software_releases.md)

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

3. Commit and push the change to the SEMIC publication repository 

**Test the result**

When the new thema repository is correctly configured then the last step will result in an update to the SEMIC generated repository. A new directory will appear: /doc/applicationprofile/DCAT-AP.

In case of errors, consult the CircleCI web interface to find the step that caused the error. The most frequent sources of problems are: 

* The JSON configuration files are not in the proper JSON syntax. In this case, a JSON formatter can be used (e.g., [jq](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwj5tpDpt_b7AhVhgc4BHTWBBXIQFnoECA8QAQ&url=https%3A%2F%2Fjqplay.org%2F&usg=AOvVaw32nsoMdEDWyJ_cAtdjZ0oz&cshid=1670929115779122), [JSON formatter and validator](https://jsonformatter.curiousconcept.com/)…)
* The configuration values refer to non-existing information like a non-existing diagram in the UML file, a non-existing template, etc.
* Usage of  special characters and whitespace characters may also be a source of problems,  but these are usually part of the data specification content. While these are the editors responsibility, the toolchain developer might be involved to find the exact source of these.

#### [<<< Previous page: Task-Deploy new software releases ](deploy_new_software_releases.md)