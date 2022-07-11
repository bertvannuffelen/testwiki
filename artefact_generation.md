#### [<<< Previous page: Actors](./actors.md) --- [Next page: Datamodel >>>](./datamodel.md)

# Artefact generation process

This chapter describes the artefact generation process for a data specification.
The target audience for this chapter are experienced editors and developers who want to understand and improve the artefact generation.
Nevertheless, novel editors are also invited to perform a quick reading, as this will help them to better communicate with the developers, when the artefact generation fails.

## Overview

The creation of the data specification artefacts is roughly a *two phase* process. 
First, all information of the data specification is collected in an internal representation. 
Next, out of that internal representation, the artefacts of the data specification to be published are generated.
The first phase is denoted as the [Aggregation phase](#1-aggregation-phase), while the second is called the [Generation phase](#2-generation-phase).


The *internal representation* has the same structure for each data specification category. 
This simplifies the developers' effort to create (new) artefact generators for (new or existing) data specifications, as experience from one generator can be transferred to another.
The internal representation contains, besides the semantic model of a data specification (see the [datamodel](./datamodel.md) chapter), also 
  -  the contributers (i.e. editor, author, collaboration) to the data specification,  and
  -  the complete configuration information associated with the data specification. 

This configuration information consists of: the data specification configuration ([see example](https://github.com/SEMICeu/uri.semic.eu-thema/blob/example/config/core-person.json)), the publication point configuration ([see example](https://github.com/SEMICeu/uri.semic.eu-publication/blob/example/config/dev/publication.json)), the publication environment configuration ([see example](https://github.com/SEMICeu/uri.semic.eu-publication/blob/example/config/config.json)), and the toolchain execution information.
The toolchain execution information consists of runtime information related to the actual CI/CD execution at the moment of processing the data specification. For instance, the commit in the publication repository that triggered the toolchain, but also the thema repository commit that identifies the data specification that is being processed.
The complete internal representation of the data specification given as example in the [editorial flow](./editorial_flow.md) chapter can be found [here](https://github.com/SEMICeu/uri.semic.eu-generated/blob/example/report/doc/core-vocabulary/core-person/all-core-person-ap.jsonld).
Storing the internal representation in the generated repository provides an opportunity for the editors to explore this structure, to detect the origin of errors, or to express new features for artefact generators.

The complete artefact generation process is automated, and it is implemented using CircleCI within the publication repository [uri.semic.eu-publication](https://github.com/SEMICeu/uri.semic.eu-publication). 
The CircleCI web application offers a visual representation of the CircleCI workflow, and thus a visual representation of the artefact generation process.
Generic information about the organisation and setup of the workflow of the CircleCI workflow is provided in the documentation of the [OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template#readme) GitHub repository.


## 1. Aggregation phase 

The _core activity_ of the first phase is the extraction of the semantic model expressed in the UML diagram into the *internal representation*.
The [datamodel](./datamodel.md) chapter describes in detail how the UML diagram expressing the semantic model of a data specification is basically a standard UML model extended with annotations.

The key component is the [UML Conversion Tool](https://github.com/Informatievlaanderen/OSLO-EA-to-RDF).
This tool is responsible for assigning PURIs to the terms in the data specification, and for the interpretation of the UML model as a semantic model.
To avoid diverging semantic interpretations across the artefacts, the generators should not make any semantic interpretation in the generation phase. 
Determining what is a class or a property, the assignment of PURIs, etc. are the sole responsability for the UML Conversion Tool, and should happen in the aggregation phase.

Besides the semantic interpretation, the aggregation phase is also handling the multilingual aspects, by creating *translation files*.
Translation files contain all translatable content in a structure that is compatible with the semantic model. 
[Here](https://github.com/SEMICeu/uri.semic.eu-generated/blob/example/report/doc/core-vocabulary/core-person/translation/core-person-ap_de.json) is an example translation file for the Core Person Vocabulary to provide the labels of the terms in German.
During the aggration phase, the provided translations are merged into the internal representation to create a language aware internal representation.



## 2. Generation phase 

The toolchain provides a number of artefact generators. 
During the generation phase, these artefact generators are executed to produce the artefacts according to the expectations of the different [data specification categories ](./datamodel.md#data-specification-categories).
The result of the generation process is stored in the generated repository under the path defined by the `urlref` provided by the publication point.
For instance, the generated artefacts for the [example publication point](https://github.com/SEMICeu/uri.semic.eu-publication/blob/example/config/dev/publication.json#L3) are found [here](https://github.com/SEMICeu/uri.semic.eu-generated/tree/example/doc/core-vocabulary/core-person).

During the editing of a data specification editors should not be concerned with the internal details of the artefact generators.
However, experienced editors may start reflecting on whether the produced artefacts will satisfy the consumers' expectations or needs.
At that moment editors become developers; namely, they will be not just editing the model, but will also be evaluating and desiging the expected outcome of the artefacts.
The provided documentation targets the knowledge required for performing editorial activities. 
Design considerations for developers are beyond scope.

Below we provide a short description for each artefact generator.

### 2.1 HTML artefact generator

The HTML artefact generator makes an HTML file by rendering the internal representation according to a template.
The objective of the HTML represenation is create a human readable representation. 
The template language used is [Nunjuncks](https://mozilla.github.io/nunjucks/).

The data specification configuration in the thema repository contains the reference to the [template](https://github.com/SEMICeu/uri.semic.eu-thema/blob/example/config/core-person.json#L7).
The template language supports modularity via importing other templates. 
The HTML artefact generator is designed and configured to exploit this mechanism, so that the data specification's specific content, e.g. the summary, is combined with a generic template for the publication environment.
The ability to work with reusable generic templates is an enabler for a coherent consumer experience on the Web.
Creating reusable generic templates requires knowledge about the publication environment, such as the hostname and path where the HTML document will be published, and where additional information, such as pictures, that are part of the data specification's content, can be accessed.
While the first is part of the publication repository configuration, the latter is part of the thema repository. 

The generation is language sensitive, as the labels, definitions and usage notes of the terms in the data specification are language sensitive.
Therefore, the language to be used from the internal representation must be specified.

Besides these key options, there are more options facilitating the implementation, but these are for the developers to explore. 


### 2.2 RDF artefact generator

The RDF artefact generator makes a JSON-LD file out of the internal representation.
Using of-the-shelf JSON-LD to RDF serialisation convertion tools the JSON-LD file is expressed as Turtle, N-Triples or RDF/XML.

The objective is to support the machine readable representation of the vocabulary terminology. This artefact is thus tightly coupled with the PURI publication process.

The generation is not language sensitive, as RDF allows multilanguage content.

### 2.3 JSON-LD context artefact generator

The JSON-LD context artefact generator creates a [JSON-LD context](https://www.w3.org/TR/json-ld/#the-context) out of the internal representation.

The objective is to create a kick start building semantically annotated JSON-based RESTful APIs. 
The REST developer community is usually not familiar with the Semantic Web.
The generated context files allow to quickly compose a JSON structure with the correct semantic mappings. 

The generation is language sensitive, as the attribute names to be mapped can be based on the labels of the terms in the data specification.
Therefore, the language to be used from the internal representation must be specified.

The generation is also sensitive to disambiguation challenges. 
It may occur that two different terms in a data specification use the same label. 
For example, consider a property _status_ used within the same data specification in two different classes, e.g. _Requirement_ and _Evidence_. 
Despite the label _status_ is unambigous in the context of each class, globally within the data specification there are differences: the codelists, usage note, the URI, etc.
To ensure that the JSON-LD context does not create unintentional overlaps, the generated JSON-LD attribute names can be disambiguated.
This is done by prefixing the labels with the domain of the class to which the property belongs. 
Forcing domain based disambiguation is switched on for the JSON-LD generator in the SEMIC toolchain.

### 2.4 SHACL artefact generator

The SHACL artefact generator creates a file containing [SHACL shapes](https://www.w3.org/TR/shacl/#shapes) out of the internal representation.

The objective is to facilitate data validation. 
By configuring a validator, e.g. the [TestBed](https://joinup.ec.europa.eu/collection/interoperability-test-bed-repository/solution/interoperability-test-bed), with the SHACL file, a data validation environment is created. 

The design of the SHACL shapes is a non-trivial process. 
The SHACL language allows to express the same collection of constraints in various ways.
In the [Webinar on DCAT-AP validation](https://joinup.ec.europa.eu/collection/semantic-interoperability-community-semic/news/shacl-shapes-dcat-ap-webinar), the impact of some expression forms have been elaborated.

A _constraint_ is an restriction on the use of the terminology in the data specification, such as, its domain, range, minimum and maximum cardinality, etc.

In the most compact representation the constraints are grouped per SHACL node.
In this design, the error messages that users of a data validation system will recieve, are those that are produced by a validator engine.
They are fixed, and cannot be altered by the SHACL shape designer.

An alternative design is to create a unique SHACL node per constraint.
In this case dedicated error messages can be associated per constraint.
This representation allows to add more easily usage notes specific constraints, such as, _there should be only one value per language_, for which SHACL has a dedicated expression.

The generation is language sensitive, as the validation messages are based on the labels of the terms in the data specification.
Therefore, the language to be used from the internal representation must be specified.
In a multilingual context, the second representation is required as it is the only way to create a error context aware message in multiple languages.

In the SEMIC toolchain the first, more compact, representation is active.


## 3. Adding a new artefact generator to the artefact generation process

The  [OSLO-Specificationgenerator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator) GitHub repository collects the OSLO artefact generators.
These are all written in JavaScript. 
A test suite is available in the repository, illustrating the usage of each artefact generator w.r.t. different parameter choices.

Adding a new artefact generator in the artefact generation process involves the following broad steps:
   1. Implement the artefact generator
       - create the new artefact generator as a new JavaScript tool
       - add the test suite
       - build and publish a new docker image with the new artefact generator included
   2. Integrate the artefact generator in the artefact generation process
       - update the CircleCI workflow
       - extend or implement supportive scripts in the publication environment
       - test the result

The integration is best applied on a working setup.  
When the new artefact generator has reached maturity, this additional generation possibility should be shared with the community, by adding it as part of a new version of the
[OSLO-publicationenvironment-template](https://github.com/Informatievlaanderen/OSLO-publicationenvironment-template).

#### [<<< Previous page: Actors](./actors.md) --- [Next page: Datamodel >>>](./datamodel.md)


