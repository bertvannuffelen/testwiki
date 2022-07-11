# XSD artefact generation

The toolchain is capable to generate different artefacts.
This section describes the creation of an XSD based on the data specification.

The SEMIC XML Open Guidelines (See [1]) describe the generic rules for building good XML structures.
The toolchain contains a generator that produces an XSD according to these guidelines. 
[3] is the current output for Core Person.

Technically the generation process is constructed as follows:

The CircleCI workflow step `render-xsd-details` (See [5]) initiates the creation of the xsd artefact creation.
Within this step the script `render-details.sh` (See [6]) is called which will execute a javascript tool for all data specifications.
This javascript tool `xsd-generator.js` (See [4]) has as input the intermediate json for the dataspecification. 
For instance, for Core Person it is this file [2].

The javascript tool implements many, but not all, rules defined in [1].
Some rules cannot be realised in automated xsd generation, such as R22 and R23.
Others require more fine-grained discussion like how to turn a label of a term into a valid XML tag name. 
The label can includes special characters like `(` or a white space, but these characters are invalid XML tag name characters.

The result of the XSD generator is thus today only partially the intended outcome. 
To resolve some issues the UML of the Core Vocabulary might have to revised, but that impacts the other artefacts.
To minimize the impact, a dedicated UML variant might be created and the outcome of that is published.
The drawback of that choice is to maintain the coherency between both UML files.
An alternative might be to apply manual changes before releasing the XSD to the public.
But also this creates a maintenance issue.



### References

- [1] [SEMIC XML Open Guidelines](https://github.com/SEMICeu/OpenGuidelines/blob/main/xml/guidelines.md)
- [2] [Example intermediate json for Core Person](https://github.com/SEMICeu/uri.semic.eu-generated/blob/master/report/doc/core-vocabulary/core-person/all-core-person-ap.jsonld)
- [3] [Example xsd for Core Person](https://github.com/SEMICeu/uri.semic.eu-generated/blob/master/doc/core-vocabulary/core-person/xsd/core-person-ap.xsd)
- [4] [Generator for xsd generator](https://github.com/Informatievlaanderen/OSLO-SpecificationGenerator/blob/multigual-dev/xsd-generator.js)
- [5] [CircleCI step triggering the xsd generation](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/.circleci/config.yml#L300)
- [6] [Toolchain script triggering the xsd generation](https://github.com/SEMICeu/uri.semic.eu-publication/blob/master/scripts/render-details.sh#L356)

