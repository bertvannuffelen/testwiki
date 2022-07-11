# Frequently Asked Questions

## Are there examples that describe the full editorial workflow?
The different HowTo sections of the Toolchain page that address various use cases, as well as the "Example workflow" page should provide
detailed examples, such as the flow from UML to final xsd, including the intermediate steps like what has to be done with references etc.

## How do I change an existing element in a vocabulary?
  -> toolchain.md
## How do I add a new element to an existing vocabulary?
  -> toolchain.md
## How do I delete an element in a vocabulary?
  -> datamodel.md
## What are the tools that one need to install to edit/publish the data specifications?
design decision: Are there alternatives for Enterprise Architect (to model UML) and circleci (as built tool)? 
  -> toolchain.md
  
## Is there a plan to offer a public PURI request service?
  -> puri.md
  
the PURI part of the ToolChain is mainly focused on technical issues: http/https, URL rewriting, Docker, etc.
semantic aspects are not discussed at all.
  -> puri.md (note that semantical discussion on puris somehow part of the background knownledge)

## What is the role of each java script file? Is there a dedicated java script file for every different serialization?
  -> yes

## Where are the different rules for the creation of the xsd serialization are defined and how they can be modified?
  -> in the javascript tool there is an implementation from the rules expressed in confluence.

## What is the minimum set of tools and files taken for the ones provided by OSLO so that SEMIC can perform its job?
  -> that is up to SEMIC to decide

## How can I create a copy of the OSLO github and run the toolchain from an virtual image locally and how I can run it through github environment?
  -> github forking/cloning.

## What are the different roles and prerequisite knowledge/skills.
-> Readme.md / Actor.md

## Do the tools that are used at the moment meet the needs of the end-user (editor role and/or others)? An even one more basic level: What does the end-user need? What are his/her skills and knowledge.
-> Readme.md

## What is already in use by the final user (editor and member of the WG) that can be re-used as tools to promote acceptance? 
Basic ideas on the perspective of the end user as a stakeholders, for example git, in terms of training.
-> no formal training exists. Same situation as before in the last 10 years.

## How can the quality of the tools be ensured?
-> By collaboration as it is open source.

## How can errors be created or fixed (e.g. the various issues in the Person XSD schema)?
-> By "artefact-generation" improval process
   -> toolchain.md 

## What is open source?  
-> all components except Enterprise architect



