#### [<<< Previous page:  Task-Editing HTML specifications ](editing_HTML_specifications.md) --- [Next page: Task-Customise the publication process >>>](customise_publication_process.md)


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

#### [<<< Previous page:  Task-Editing HTML specifications ](editing_HTML_specifications.md) --- [Next page: Task-Customise the publication process >>>](customise_publication_process.md)
