#### [<<< Homepage](https://github.com/SEMICeu/documentation) --- [Next page: Artefact generation >>>](./artefact_generation.md)

# Actors

There are three main types of actors that will interact with the resources and assets produced and managed by SEMIC on the SEMICeu GitHub space: the data specification _consumers_, the data specification _editors_, and the supporting asset _developers_. 

The connection between these three group of actors is the following: The tools and methods are set up by the _developers_ to support the _editors_ in their work, to provide together a coherent experience to the _consumers_.

Since the _consumers_ are the "end users" of the data specifications, they will not need to interact directly with the SEMICeu GitHub space. 
Therefore, this page will focus mostly on defining the roles of the _editors_ and _developers_, and will provide less details about _consumers_ and other user roles.

The page is structured in sections and subsections describing these **roles** and their related **activities**, as follows:

1. [Consumers](#consumers)
2. [Editors](#editors)
3. [Developers](#developers)
4. [Other roles](#other-roles)
    1. [Communication](#communication)
	2. [User access management](#access-management)




## Consumers 

The main group of consumers of the data specifications are the EU Member State administrations that want to exchange data cross-border.
To support that activity an EU wide understanding of the semantics of the shared data is required.
SEMIC offers a platform to achieve a consensus on the semantics, and the result is being published as a *data specification*.

Although the EU Member State administrations are the main target audience, the work and participation is open to anybody. 
So, a consumer can also be an enterprise doing business in Japan, for example.


## Editors

The key users of the tooling and methods are the _editors_ of data specifications. 
They are expected to have the following skills:   

 - can write “formal” statements in vocabularies & application profiles (***linguistic skills***)  
 - can organise information in a data model (***structuring skills***)  
 - can explain data modelling issues in a webinar (***communication skills***)  
 - can write & execute simple software code (***software developer skills***)  

The editors should be familiar with the Semantic Web.
That is, they should have knowledge and experience with the terminology, the data formats and tools used in the Semantic Web community. 
This documentation is not targeting editors who model a data specification (according to the Semantic Web principles) for the first time.
Nevertheless, with a coach, and by using the tooling, editors with limited experience can become more experienced quite quickly. 


The objective of the provided tooling and processes is that editors focus on their main task; namely, on improving and maintaining the data specification and interacting with the working group communities.    

A key non-functional requirement for the tooling is that it should not create bottlenecks that prevent the scaling up of the editorial effort. 
Therefore, local installation of software and data should be avoided. 
The maintenance of the data specification should never be blocked because one editor has sole access to data.

Also, at any point in time it should be clear what is the technical content on which the data specification is build. 
Any knowledge transfer between editors can then be focussed on sharing the current expertise on the different opinions in the working group instead of figuring out how to pass technical artifacts. 


## Developers

_Developers_ are the supporting actors in this story.
Their role is mainly to be able to assist in resolving any technical issue with the setup. 
Thus, the performed activities are primarily of operational nature, and less oriented to new development.
When it comes to new development, this will be mostly in the area of automation. 
As mentioned in the [Historical Background](README.md#historical-background), the SEMIC tooling and organisation is grown step by step. 
To support the editors even better more automation is required.


The prerequisite knowledge of a developer can be circumscribed as being a Swiss knife (or a full-stack) developer.
Developers (or the developers team) should have the following skills:

 - have generic programming skills
 - being able to process, read and manipulate software in different programming languages and development setups, e.g. Bash, JavaScript, HTML, JSON, Nginx, Apache 
 - being able to read documentation of various tools and search for missing documentation on the Web, e.g. Nunjucks
 - understand and work with Continuous Integration and Continuous Development (CI/CD) tools, e.g. [CircleCI](https://circleci.com/)
 - understand and work in the spirit of "infrastructure as code", and be able to operate and deploy software using Docker containers, e.g. Docker, Docker Compose 
 - be familiar with the Linux ecosystem, able to explore and execute tasks via command line, e.g. Ubuntu
 - have affinity with the Semantic Web, e.g. RDF serialisations (N-Triples, Turtle, RDF/XML), SPARQL, Virtuoso, JSON-LD, dereferencing URIs
  
The work environment that the editors are faced with is more uniform than those by the developers. 
It is advised to maintain the highest burden on the developers and not make design decisions that make the developers life easier, but complicate the work of the editors.
For instance, the usage of GitHub repositories to store the data specifications, should not be the reason to impose a software development approach on those GitHub repositories. 
The organisation and management of those repositories should match the needs of the editors and the publication objectives. 
For instance, whereas for software the scope of a branch in a repository is to ensure that work always happens on a coherent set of instructions, in case of a data specification the scope is to keep a transparent record of the history of the specification. 


## Other roles
Besides the main roles that the above described actors have to fulfil, there exist also other roles, involving specific activities, that certain actors need to assume. These activities are described below.

### Communication
Besides the activities related to the creation and management of the data specifications, there are also __communication activities__, like publishing the results on JoinUp.

These are not documented here (yet).

### Access management

For the different actors to be able to perform the activities implied by their roles, they need to have access to the various SEMIC assets.
Therefore, there is a need for a proper user access management.

For the activities described in this documentation _editors_ only require write permissions to the SEMIC GitHub space.
To facilitate the access management of people with editorial role, an [editors team](https://github.com/orgs/SEMICeu/teams/core-voc-editors) has been created in the SEMIC GitHub space.

_Developers_ usually are granted more extensive rights to perform the various tasks on the SEMIC assets. 
For them, and the EC officials, the [SEMIC administrators team](https://github.com/orgs/SEMICeu/teams/administrators) was set up.
They have full access to the SEMIC GitHub space.
They can also perform any necessary access control operation for individual users.

#### [<<< Homepage](https://github.com/SEMICeu/documentation) --- [Next page: Artefact generation >>>](./artefact_generation.md)




