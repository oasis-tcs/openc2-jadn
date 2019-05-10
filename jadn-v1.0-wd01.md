
![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v2.0.jpg)
-------

# Specification for JSON Abstract Data Notation Version 1.0

## Working Draft 01

## 10 May 2019

### Technical Committee:
* [OASIS Open Command and Control (OpenC2) TC](https://www.oasis-open.org/committees/openc2/)

### Chairs:
* Joe Brule (jmbrule@radium.ncsc.mil), [National Security Agency](https://www.nsa.gov/)
* Duncan Sparrell (duncan@sfractal.com), [sFractal Consulting LLC](http://www.sfractal.com/)

### Editor:
* David Kemp (dkemp@mobility-challenge.com), [National Security Agency](https://www.nsa.gov/)

### Additional artifacts:
This prose specification is one component of a Work Product that also includes:

* Schema for JADN specifications
* Conformance test data
* Examples

### Abstract:
JSON Abstract Data Notation (JADN) is an information modeling language based on the CBOR data model. It has several purposes, including definition of data structures, validation of data instances, providing hints for user interfaces working with structured data, and facilitating protocol internationalization. JADN specifications consist of two parts: abstract type definitions that are independent of data format, and serialization rules that define how to represent type instances using specific data formats. A JADN schema is itself a structured information object that can be serialized and transferred between applications, documented in multiple formats such as property tables and text-based data definition languages, and translated into concrete schemas used to validate specific data formats.

### Status:
This document was last revised or approved by the OASIS Open Command and Control (OpenC2) TC on the above date. The level of approval is also listed above. Check the "Latest version" location noted above for possible later revisions of this document. Any other numbered Versions and other technical work produced by the Technical Committee (TC) are listed at https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2#technical.

TC members should send comments on this specification to the TC's email list. Others should send comments to the TC's public comment list, after subscribing to it by following the instructions at the "Send A Comment" button on the TC's web page at https://www.oasis-open.org/committees/openc2/.

This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode) Mode of the OASIS IPR Policy, the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page (https://www.oasis-open.org/committees/openc2/ipr.php).

Note that any machine-readable content ([Computer Language Definitions](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsCompLang)) declared Normative for this Work Product is provided in separate plain text files. In the event of a discrepancy between any such plain text file and display content in the Work Product's prose narrative document(s), the content in the separate plain text file prevails.

### URI patterns:
Initial publication URI:  
https://docs.oasis-open.org/openc2/jadn/v1.0/csd01/jadn-v1.0-csd01.html

Permanent "Latest version" URI:  
https://docs.oasis-open.org/openc2/jadn/v1.0/jadn-v1.0.html

### Citation format:
When referencing this specification the following citation format should be used:

**[JADN-v1.0]**

_Specification for JSON Abstract Data Notation Version 1.0_. Edited by David Kemp. 01 March 2019. OASIS Committee Specification Draft 01. https://docs.oasis-open.org/openc2/jadn/v1.0/csd01/jadn-v1.0-csd01.html. Latest version: https://docs.oasis-open.org/openc2/jadn/v1.0/jadn-v1.0.html.

-------

## Notices
Copyright © OASIS Open 2019. All Rights Reserved.

All capitalized terms in the following text have the meanings assigned to them in the OASIS Intellectual Property Rights Policy (the "OASIS IPR Policy"). The full [Policy](https://www.oasis-open.org/policies-guidelines/ipr) may be found at the OASIS website.

This document and translations of it may be copied and furnished to others, and derivative works that comment on or otherwise explain it or assist in its implementation may be prepared, copied, published, and distributed, in whole or in part, without restriction of any kind, provided that the above copyright notice and this section are included on all such copies and derivative works. However, this document itself may not be modified in any way, including by removing the copyright notice or references to OASIS, except as needed for the purpose of developing any document or deliverable produced by an OASIS Technical Committee (in which case the rules applicable to copyrights, as set forth in the OASIS IPR Policy, must be followed) or as required to translate it into languages other than English.

The limited permissions granted above are perpetual and will not be revoked by OASIS or its successors or assigns.

This document and the information contained herein is provided on an "AS IS" basis and OASIS DISCLAIMS ALL WARRANTIES, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTY THAT THE USE OF THE INFORMATION HEREIN WILL NOT INFRINGE ANY OWNERSHIP RIGHTS OR ANY IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE.

OASIS requests that any OASIS Party or any other party that believes it has patent claims that would necessarily be infringed by implementations of this OASIS Committee Specification or OASIS Standard, to notify OASIS TC Administrator and provide an indication of its willingness to grant patent licenses to such patent claims in a manner consistent with the IPR Mode of the OASIS Technical Committee that produced this specification.

OASIS invites any party to contact the OASIS TC Administrator if it is aware of a claim of ownership of any patent claims that would necessarily be infringed by implementations of this specification by a patent holder that is not willing to provide a license to such patent claims in a manner consistent with the IPR Mode of the OASIS Technical Committee that produced this specification. OASIS may include such claims on its website, but disclaims any obligation to do so.

OASIS takes no position regarding the validity or scope of any intellectual property or other rights that might be claimed to pertain to the implementation or use of the technology described in this document or the extent to which any license under such rights might or might not be available; neither does it represent that it has made any effort to identify any such rights. Information on OASIS' procedures with respect to rights in any document or deliverable produced by an OASIS Technical Committee can be found on the OASIS website. Copies of claims of rights made available for publication and any assurances of licenses to be made available, or the result of an attempt made to obtain a general license or permission for the use of such proprietary rights by implementers or users of this OASIS Committee Specification or OASIS Standard, can be obtained from the OASIS TC Administrator. OASIS makes no representation that any information or list of intellectual property rights will at any time be complete, or that any claims in such list are, in fact, Essential Claims.

The name "OASIS" is a trademark of [OASIS](https://www.oasis-open.org/), the owner and developer of this specification, and should be used only to refer to the organization and its official outputs. OASIS welcomes reference to, and implementation and use of, specifications, while reserving the right to enforce its marks against misleading uses. Please see https://www.oasis-open.org/policies-guidelines/trademark for above guidance.

-------

# Table of Contents
[[TOC will be inserted here]]

-------

# 1 Introduction

Many standards are developed using data definition tables with the goal of being agnostic of transfer format, but no well-defined mechanism exists for achieving that goal. JADN is a schema language with definitions that can be both validated for correctness and documented in table format, ensuring that table content is valid. A JADN schema is executable byte code that can be transferred between applications, interpreted to validate application data, and embedded to produce self-describing data.

Numerous data definition languages are in use. JADN is not intended to replace any of them, but serves as a Rosetta stone to facilitate translation among them.

## 1.1 IPR Policy
This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode) Mode of the [OASIS IPR Policy](https://www.oasis-open.org/policies-guidelines/ipr), the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page ([https://www.oasis-open.org/committees/openc2/ipr.php](https://www.oasis-open.org/committees/openc2/ipr.php)).

## 1.2 Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [[RFC2119](#rfc2119)] and [[RFC8174](#rfc8174)] when, and only when, they appear in all capitals, as shown here.

## 1.3 Normative References
###### [ES9]
ECMA International, *"ECMAScript 2018 Language Specification"*, ECMA-262 9th Edition, June 2018, https://www.ecma-international.org/ecma-262.
###### [EUI]
"IEEE Registration Authority Guidelines for use of EUI, OUI, and CID", IEEE, August 2017, https://standards.ieee.org/content/dam/ieee-standards/standards/web/documents/tutorials/eui.pdf.
###### [RFC791]
Postel, J., "Internet Protocol", RFC 791, September 1981, http://www.rfc-editor.org/info/rfc791.
###### [RFC2119]
Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997, http://www.rfc-editor.org/info/rfc2119.
###### [RFC2673]
Crawford, M., *"Binary Labels in the Domain Name System"*, RFC 2673, August 1999, https://tools.ietf.org/html/rfc2673.
###### [RFC4291]
Hinden, R., Deering, S., "IP Version 6 Addressing Architecture", RFC 4291, February 2006, http://www.rfc-editor.org/info/rfc4291.
###### [RFC4632]
Fuller, V., Li, T., "Classless Inter-domain Routing (CIDR): The Internet Address Assignment and Aggregation Plan", RFC 4632, August 2006, http://www.rfc-editor.org/info/rfc4632.
###### [RFC4648]
Josefsson, S., "The Base16, Base32, and Base64 Data Encodings", RFC 4648, October 2006, http://www.rfc-editor.org/info/rfc4648.
###### [RFC5234]
Crocker, D., Overell, P., *"Augmented BNF for Syntax Specifications: ABNF"*, RFC 5234, January 2008, https://tools.ietf.org/html/rfc5234.
###### [RFC7049]
Bormann, C., Hoffman, P., *"Concise Binary Object Representation (CBOR)"*, RFC 7049, October 2013, https://tools.ietf.org/html/rfc7049.
###### [RFC8174]
Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174, May 2017, http://www.rfc-editor.org/info/rfc8174.
###### [RFC8200]
Deering, S., Hinden, R., "Internet Protocol, Version 6 (IPv6) Specification", RFC 8200, July 2017, http://www.rfc-editor.org/info/rfc8200.
###### [RFC8259]
Bray, T., "The JavaScript Object Notation (JSON) Data Interchange Format", STD 90, RFC 8259, December 2017, http://www.rfc-editor.org/info/rfc8259.

## 1.4 Non-Normative References
###### [AVRO]
Apache Software Foundation, *"Apache Avro Documentation"*, https://avro.apache.org/docs/current/.
###### [CDDL]
Birkholz, H., Vigano, C., Bormann, C., *"Concise Data Definition Language"*, Internet-Draft, July 2017, https://tools.ietf.org/html/draft-ietf-cbor-cddl-07.
###### [DRY]
*"Don't Repeat Yourself"*, https://en.wikipedia.org/wiki/Don%27t_repeat_yourself.
###### [GFM]
*"GitHub Flavored Markdown"*, https://github.github.com/gfm/.
###### [JSONSCHEMA]
Wright, A., Andrews, H., Luff, G., *"JSON Schema Validation"*, Internet-Draft, March 2018, https://tools.ietf.org/html/draft-handrews-json-schema-validation-01.
###### [MDA]
Cephas Consulting Group, *"The Fast Guide to Model Driven Architecture"*, https://www.omg.org/mda/mda_files/Cephas_MDA_Fast_Guide.pdf.
###### [PROTO]
Google Developers, *"Protocol Buffers"*, https://developers.google.com/protocol-buffers/.
###### [RELAXNG]
OASIS Technical Committee, *"RELAX NG"*, November 2002, https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=relax-ng.
###### [RFC3444]
Pras, A., Schoenwaelder, J., *"On the Difference between Information Models and Data Models"*, RFC 3444, January 2003, https://tools.ietf.org/html/rfc3444.
###### [RFC3552]
Rescorla, E. and B. Korver, "Guidelines for Writing RFC Text on Security Considerations", BCP 72, RFC 3552, DOI 10.17487/RFC3552, July 2003, https://www.rfc-editor.org/info/rfc3552.
###### [RFC7493]
Bray, T., "The I-JSON Message Format", RFC 7493, March 2015, https://tools.ietf.org/html/rfc7493.
###### [THRIFT]
Apache Software Foundation, *"Writing a .thrift file"*, https://thrift-tutorial.readthedocs.io/en/latest/thrift-file.html.
###### [UML]
"UML Multiplicity and Collections", https://www.uml-diagrams.org/multiplicity.html.

-------

# 2 Information vs. Data
JSON Abstract Data Notation (JADN) is an information modeling language. 
[RFC 3444](#rfc3444) describes the difference between an information model (IM) and a data model (DM):
* The main purpose of an IM is to model managed objects at a conceptual level,
independent of any specific implementations or protocols used to transport
the data.
* DMs, conversely, are defined at a lower level of abstraction and include
many details. They are intended for implementors and include protocol-specific
constructs.
```
             IM                --> conceptual/abstract model
              |                    for designers and operators
   +----------+---------+
   |          |         |
   DM        DM         DM     --> concrete/detailed model
                                   for implementors
```
Since conceptual models can be implemented in different ways, multiple DMs
can be derived from a single IM.

Within a Model Driven Architecture ([MDA](#mda)):
* An IM is part of a Platform Independent Model (PIM) that exhibits a sufficient degree of independence so as to enable its
mapping to one or more platforms.
* A DM is part of a Platform Specific Model (PSM) that combines the specifications in the PIM with the details
required to stipulate how a system uses a particular type of platform. 

Information is *what* needs to be communicated between applications, and data is *how* that information
is represented when communicating.  More formally, information is the unexpected data, or "entropy",
contained in a message.  When information is serialized for transmission in a canonical format, the additional
data used for purposes such as text conversion, delimiting, and framing contains no information because it is known a priori.
If the serialization is non-canonical, any additional entropy introduced during serialization
(e.g., whitespace, leading zeroes, reordering, case-insensitive capitalization) is discarded on deserialization.

For example, an IPv4 address contains 32 bits of information*. But different data may be used to
represent the same information:
* IPv4 dotted-quad contained in a JSON string: "192.168.141.240" (17 bytes / 136 bits).
* Hex value contained in a JSON string: "C0A88DF0" (10 bytes / 80 bits)
* CBOR byte string: 0x44c0a88df0 (5 bytes / 40 bits).
* IPv4 packet: 0xc0a88df0 (4 bytes / 32 bits).

In an IM, an IPv4 address is always *defined* to be a 32 bit value regardless the DMs used to *represent* it for processing within applications, communication among applications, or storage.

\* *Note: all references to information in this document assume uniform distribution over all possible values.*

**Information Modeling**

JADN is based on the [CBOR](#rfc7049) data model ([JSON](#rfc8259) types plus integers, special numbers, and byte strings), but has an
information-centric focus:

| Data-centric | Information-centric |
| --- | --- |
| A data definition language is designed around specific data formats. | An information modeling language is designed to express application needs. |
| Serialization-specific details are built into applications. | Serialization is a communication function like compression and encryption, provided to applications. |
| JSON Schema defines integer as a value constraint on the JSON number type: "integer matches any number with a zero fractional part". | Integer and Number first-class types exist regardless of data representation. |
| CDDL says: "While CBOR map and array are only two representation formats, they are used to specify four loosely-distinguishable styles of composition". | First-class types are based on five distinct composition styles.  Each type can be represented in multiple data formats. |
| No table composition style is defined. | Tables are a fundamental way of organizing information. The Record first class type holds tabular information that can be represented as both arrays and maps in multiple data formats. |
| Data-centric design is often Anglocentric, embedding English-language identifiers in protocol data. | Information-centric design encourages definition of natural-language-agnostic protocols while supporting localized identifiers within applications. |

**Implementation**

Two general approaches can be used to implement IM-based protocol specifications:
1) Translate the IM to a data-format-specific schema language such [Relax-NG](#relaxng), [JSON Schema](#jsonschema), [Protobuf](#proto), or [CDDL](#cddl), then use format-specific serialization and validation libraries to process data in the selected format. Applications use data objects specific to each serialization format.
2) Use the IM directly as a format-independent schema language, using IM serialization and validation libraries to process data without separate schema generation or code generation steps. Applications use the same IM instances regardless of serialization format.

Implementations based on serialization-specific code interoperate with those using an IM serialization library, allowing developers to select either approach. 

# 3 JADN Types
JADN first-class types are defined in terms of their characteristics; applications may use any programming language variable types or mechanisms that support those characteristics.

###### Table 3-1. JADN Types

| JADN Type | Definition |
| :--- | :--- |
| **Simple** |   |
| Binary | A sequence of octets.  Length is the number of octets. |
| Boolean | An element with one of two values: true or false. |
| Integer | A positive or negative whole number. |
| Number | A real number. |
| Null | An unspecified or non-existent value. |
| String | A sequence of characters, each of which has a Unicode codepoint.  Length is the number of characters. |
| **Compound** |   |
| Enumerated | One value selected from a set of named or labeled integers. |
| Choice | One key and value selected from a set of named or labeled fields. The key has an id and name or label, and is mapped to a type. |
| Array | An ordered list of labeled fields with positionally-defined semantics. Each field has a position, label, and type. Corresponds to CDDL *record*. |
| ArrayOf(*vtype*) | An ordered list of fields with the same semantics. Each field has a position and type *vtype*. Corresponds to CDDL *vector*. |
| Map | An unordered map from a set of specified keys to values with semantics bound to each key. Each key has an id and name or label, and is mapped to a type. Corresponds to CDDL *struct*. |
| MapOf(*ktype*, *vtype*) | An unordered map from a set of keys to values with the same semantics. Each key has key type *ktype*, and is mapped to value type *vtype*. Represents a map with keys that are either enumerated or are members of a well-defined category. Corresponds to CDDL *table*. |
| Record | An ordered map from a list of keys with positions to values with positionally-defined semantics. Each key has a position and name, and is mapped to a type. Represents a row in a spreadsheet or database table. CDDL does not have a corresponding composition style. |

The mechanisms chosen by a developer or defined by an IM library to represent these types within an application constitute an IM application programming interface (API). Serialization is the process that translates between an API value and a serialized value. JADN types are the point of convergence between multiple programming language APIs and multiple serialization formats -- Python and C++ and Java APIs define how applications represent instances of Binary data, and JSON and CBOR and XML serialization rules define how instances of Binary data are serialized:

| Python IM API |  JADN Type  |   Serialization Rules |
| ------------- | ----------- | ----------------|
| bytes<br>bytearray | Binary | JSON string (base64, hex, or other)<br>CBOR #2 byte string |
| True          | Boolean     | JSON true<br>CBOR #7.21 |
| ... | |

## 3.1 Type Definitions
JADN type definitions have a regular structure designed to be easily describable, easily processed, and extensible. Every definition creates a *Defined type* that has four elements, plus for some types, a list of fields:

1. **TypeName:** the name of the type being defined
2. **BaseType:** the JADN type ([Table 3-1](#table-3-1-jadn-types)) of the type being defined, or the name of a Defined type
3. **TypeOptions:** an array of zero or more **TypeOption** ([Table 3-2](#table-3-2-type-options)) applicable to the type being defined
4. **TypeDescription:** a non-normative comment
5. **Fields:** an array of one or more field definitions, if applicable to BaseType

* TypeName MUST NOT be a JADN type ([Table 3-1](#table-3-1-jadn-types)).
* If BaseType is a Simple type, ArrayOf, MapOf, or a Defined type, the type definition MUST NOT include Fields:
```
[TypeName, BaseType, [TypeOption, ...], TypeDescription]
```

* If BaseType is Enumerated, each field definition MUST have three elements:
1. **FieldID:** the integer identifier of the field
2. **FieldName:** the name or label of the field
3. **FieldDescription:** a non-normative comment
```
[TypeName, BaseType, [TypeOption, ...], TypeDescription, [
    [FieldID, FieldName, FieldDescription],
    ...
]]
```
* If BaseType is Array, Choice, Map, or Record, each field definition MUST have five elements:
1. **FieldID:** the integer identifier of the field
2. **FieldName:** the name or label of the field
3. **FieldType:** the type of the field
4. **FieldOptions:** an array of zero or more **FieldOption** ([Table 3-5](#table-3-5-field-options)) or **TypeOption** ([Table 3-2](#table-3-2-type-options)) applicable to the field
5. **FieldDescription:** a non-normative comment
```
[TypeName, BaseType, [TypeOption, ...], TypeDescription, [
    [FieldID, FieldName, FieldType, [FieldOption, TypeOption, ...], FieldDescription],
    ...
]]
```
* FieldType MUST be a Simple type, ArrayOf, MapOf, or a Defined type.
* FieldID and FieldName values MUST be unique within a type definition.
* If BaseType is Array or Record, FieldID MUST be the position of the field within the type, numbered consecutively starting at 1.

If BaseType is Enumerated, Choice, or Map, FieldID MAY be any nonconflicting integer tag.

### 3.1.1 Naming Requirements
JADN does not restrict the syntax of TypeName and FieldName, but naming requirements can aid readability of specifications by highlighting inconsistencies. JADN-based specifications MAY define their own name format requirements.
* Specifications that define name formats MUST define:
    * The permitted format for TypeName
    * The permitted format for FieldName
    * A Field Separator character not permitted in FieldName, used to serialize qualified field names
    * A "System" character permitted in TypeName but reserved for use in tool-generated type names
* Specifications that do not define an alternate name format MUST use the definitions in Figure 3-1 expressed in [ABNF](#rfc5234) and [Regular Expression](#es9) formats:
```
ABNF:
TypeName   = UC *31("-" / UC / LC / DIGIT / Sys)   ; e.g., Color-Values, length = 1-32 characters
FieldName  = LC *31("_" / UC / LC / DIGIT)         ; e.g., color_values, length = 1-32 characters
FieldSep   = "/"      ; 'SOLIDUS' (U+002F), Path separator for qualified field names, not allowed in FieldName
Sys        = "$"      ; 'DOLLAR SIGN' (U+0024), Reserved for tool-generated type names, e.g., $Colors.
UC         = %x41-5A  ; A-Z
LC         = %x61-7A  ; a-z
DIGIT      = %x30-39  ; 0-9

Regular Expression:
TypeName:  ^([A-Z]([-A-Za-z0-9]|\$){,31})$
FieldName: ^([a-z][_A-Za-z0-9]{,31})$
```
###### Figure 3-1: JADN Default Name Syntax in ABNF and Regular Expression Formats

Specifications MAY define the same syntax for TypeName and FieldName; using distinct formats is not needed to unambiguously parse type definitions but a visual difference can aid understanding.

### 3.1.2 Examples

JADN type definitions are themselves information objects that can be represented in many ways. [Section 5.1](#5-1-type-definition-styles) defines several styles that can be applied to type definitions in much the same manner as css styles are applied to html documents. The [Protobuf](#proto) introduction has an example Person structure with three fields, the third of which is optional. Corresponding JADN representations include:

**JADN definition of Person:**
```
["Person", "Record", [], "", [
    [1, "name", "String", [], ""],
    [2, "id", "Integer", [], ""],
    [3, "email", "String", ["[0"], ""]
]]
```

**JADN definition of Person in [GFM](#gfm) table style ([Section 5.1.1](#511-table-style)):**

  *Type: Person (Record)*

|  ID  |    Name   |   Type  |   #  | Description |
| ---: | --------- | ------- | ---: | ----------- |
|   1  | **name**  | String  |    1 |             |
|   2  | **id**    | Integer |    1 |             |
|   3  | **email** | String  | 0..1 |             |

**JADN definition of Person in JADN IDL style ([Section 5.1.2](#512-idl-style)):**
```
Person = Record {
  1 name   String,
  2 id     Integer,
  3 email  String optional
}
```

**JADN definition of Person in a hypothetical [Thrift](#thrift)-like IDL style:**
```
record Person {
  1: string name,
  2: int id,
  3: optional string email
}
```
These examples represent the same IM definition, but conformance is based on JSON definitions, which can be read unambiguously by applications with no language-specific parser. JADN definitions in JSON format are authoritative; specifications that include JADN definitions in another format SHOULD also make them available in JSON format.

## 3.2 Options
This section defines the mechanism used to support a varied set of information needs within the strictly regular structure of [Section 3.1](#31-type-definitions). New requirements can be accommodated by defining new options without modifying that structure.

Each option is a text string that may be included in TypeOptions or FieldOptions. The first character of the string is the option ID as defined in [Table 3-2](#table-3-2-type-options) and [Table 3-5](#table-3-5-field-options). The remaining characters are the value of that option, if any.

### 3.2.1 Type Options
Type options apply to the type definition as a whole. Structural options are intrinsic elements of the types defined in ([Table 3-1](#table-3-1-jadn-types)). Validation options are optional; if present they constrain which data values are instances of the defined type.

###### Table 3-2. Type Options

| ID | Label | Type | Definition |
| --- | --- | --- | --- |
|  **Structural** | | | |
| 0x3d `'='` | id | none | If present, FieldName is a suggested label rather than an immutable name |
| 0x2a `'*'` | vtype | string | Value type for ArrayOf and MapOf |
| 0x2b `'+'` | ktype | string | Key type for MapOf |
| 0x24 `'$'` | enum | string | Enumerated type derived from the specified Array, Choice, Map or Record type |
| **Validation** | | | |
| 0x2f `'/'` | format | string | Semantic validation keyword from [Section 3.2.1.3](#3213-semantic-validation-keywords) |
| 0x25 `'%'` | pattern | string | Regular expression used to validate a String type ([Section 3.2.1.4](#3214-patterns) |
| 0x7b `'{'` | minv | integer | Minimum numeric value, octet or character count, or element count |
| 0x7d `'}'` | maxv | integer | Maximum numeric value, octet or character count, or element count |
| 0x21 `'!'` | default | string | Default value for an instance of this type |

* TypeOptions MUST contain zero or one instance of each type option.
* TypeOptions MUST contain only TypeOptions allowed for BaseType as shown in Table 3-3.
* If BaseType is ArrayOf, TypeOptions MUST include a *vtype* option.
* If BaseType is MapOf, TypeOptions MUST include *ktype* and *vtype* options.

###### Table 3-3. Allowed Options

| BaseType | Allowed Options |
| :--- | :--- |
| Binary | minv, maxv, format |
| Boolean | |
| Integer | minv, maxv, format |
| Number | minv, maxv, format |
| Null | |
| String | minv, maxv, format, pattern |
| Enumerated | id, enum |
| Choice | id |
| Array | format |
| ArrayOf | vtype, minv, maxv |
| Map | id, minv, maxv |
| MapOf | ktype, vtype, minv, maxv |
| Record | |

#### 3.2.1.1 Field Identifiers

Each field in a type definition includes both FieldID and FieldName. The Enumerated, Choice, and Map types have an *id* option that determines which identifier is used in API instances of these types. If the *id* option is absent, API instances use FieldName and the type is referred to as "named". If the *id* option is present, API instances use FieldID and the type is referred to as "labeled". The Record type is always named and has no *id* option; the Array type is its labeled equivalent.
* In named types, FieldName is a defined name that is included in the semantics of the type, must be populated in the type definition, may appear in serialized data, and cannot be changed without affecting interoperability.
* In labeled types, FieldName is a suggested label that is not included in the semantics of the type, may be empty in the type definition, never appears in serialized data, and may be freely customized without affecting interoperability.

For example an Enumerated list of HTTP status codes could include the field [403, "Forbidden"].  If the type definition does not include the *id* option, serialization rules determine whether FieldID or FieldName is used in protocol data, and the name "Forbidden" cannot be changed. With the *id* option the FieldID 403 is always used in protocol data, but the label "Forbidden" may be displayed in messages or user interfaces, as could customized labels such as "NotAllowed", "Verboten", or "Interdit".

#### 3.2.1.2 Value Type

The *vtype* option specifies the type of each field in an ArrayOf or MapOf type. It may be any JADN type or Defined type.
* An ArrayOf or MapOf instance MUST be considered invalid if any of its elements is not an instance of *vtype*.

#### 3.2.1.3 Key Type
The *ktype* option specifies the type of each key in a MapOf type. 
* *ktype* SHOULD be a Defined type, either an enumeration or a type with constraints that specify a fixed subset of values that belong to a category.
* A MapOf instance MUST be considered invalid if any of its keys is not an instance of *ktype*.

#### 3.2.1.4 Derived Enumeration
The *enum* option is a schema optimization that creates an Enumerated type derived from a referenced Array, Choice, Map or Record type. (See [Section 3.3](#33-type-simplification)).

#### 3.2.1.5 Semantic Validation
The *format* option value is a semantic validation keyword. Each keyword specifies validation requirements for
a fixed subset of values that are accurately described by authoritative resources.  The *format* option may also
affect how values are serialized, see [Section 4](#4-serialization).

###### Table 3-4. Semantic Validation Keywords
| Keyword      | Type   | Requirement |
| ------------ | ------ | ------------|
| **[JSON Schema](#jsonschema)*** **format**   | | |
| date-time    | String | [RFC 3339](#rfc3339) Section 5.6 |
| date         | String | [RFC 3339](#rfc3339) Section 5.6 |
| time         | String | [RFC 3339](#rfc3339) Section 5.6 |
| email        | String | [RFC 5322](#rfc5322) Section 3.4.1 |
| idn-email    | String | [RFC 6531](#rfc6531), or email |
| hostname     | String | [RFC 1034](#rfc1034) Section 3.1 |
| idn-hostname | String | [RFC 5890](#rfc5890) Section 2.3.2.3, or hostname |
| ipv4         | String | [RFC 2673](#rfc2673) Section 3.2 "dotted-quad" |
| ipv6         | String | [RFC 4291](#rfc4291) Section 2.2 "IPv6 address" |
| uri          | String | [RFC 3986](#rfc3986) |
| uri-reference| String | [RFC 3986](#rfc3986), or uri |
| iri          | String | [RFC 3987](#rfc3987) |
| iri-reference| String | [RFC 3987](#rfc3987) |
| uri-template | String | [RFC 6570](#rfc6570) |
| json-pointer | String | [RFC 6901](#rfc6901) Section 5 |
| relative-json-pointer | String | [JSONP](#jsonp) |
| regex        | String | [ECMA 262](#es9) |
| **JADN format** | | |
| eui          | Binary | IEEE Extended Unique Identifier (MAC Address), EUI-48 or EUI-64 as specified in [EUI](#eui) |
| ipv4-addr    | Binary | IPv4 address as specified in [RFC 791](#rfc791) Section 3.1 |
| ipv6-addr    | Binary | IPv6 address as specified in [RFC 8200](#rfc8200)  Section 3 |
| ipv4-net     | Array  | Binary IPv4 address and Integer prefix length as specified in [RFC 4632](#rfc4632) Section 3.1 |
| ipv6-net     | Array  | Binary IPv6 address and Integer prefix length as specified in [RFC 4291](#rfc4291) Section 2.3 |
| i8           | Integer | Signed 8 bit integer, value must be between -128 and 127.
| i16          | Integer | Signed 16 bit integer, value must be between -32768 and 32767.
| i32          | Integer | Signed 32 bit integer, value must be between ... and ...
| u\<*n*\>     | Integer | Unsigned integer or bit field of \<*n*\> bits, value must be between 0 and 2^\<*n*\> - 1.

* *Note: There is currently no referenceable standard for JSON Schema. When one is available, it will*
*be referenced as an authoritative source of semantic validation keywords.*

#### 3.2.1.6 Pattern
The *pattern* option specifies a regular expression used to validate a String instance.
* The *pattern* value SHOULD conform to the Pattern grammar of [ECMAScript](#es9) Section 21.2.
* A String instance MUST be considered invalid if it does not match the regular expression specified by *pattern*.

#### 3.2.1.7 Size and Value Constraints
The *minv* and *maxv* options specify size or value limits.

* For Binary, String, ArrayOf, Map, or MapOf types:
    * if *minv* is not present, the lower size limit defaults to zero.
    * if *maxv* is not present or zero, the upper size limit is unspecified and defaults to an implementation-specific large number.
    * a Binary instance MUST be considered invalid if its number of bytes is less than *minv* or greater than *maxv*.
    * a String instance MUST be considered invalid if its number of characters is less than *minv* or greater than *maxv*.
    * an ArrayOf, Map, or MapOf instance MUST be considered invalid if its number of elements is less than *minv* or greater than *maxv*.

* For Integer or Number types:
    * if *minv* is present, an instance MUST be considered invalid if its value is less than *minv*.
    * if *maxv* is present, an instance MUST be considered invalid if its value is greater than *maxv*.

#### 3.2.1.8 Default Value
The *default* option is reserved for future use. It is intended to specify the value a receiving application uses for an optional field if an instance does not include its value.

### 3.2.2 Field Options
Field options apply to each field within a type definition. Each option in Table 3-5 is a structural element of the type definition.

###### Table 3-5. Field Options

| ID | Label | Type | Definition |
| --- | --- | --- | --- |
| 0x5b `'['` | minc | integer | Minimum cardinality |
| 0x5d `']'` | maxc | integer | Maximum cardinality |
| 0x26 `'&'` | tfield | enum | Field that specifies the type of this field |
| 0x3c `'<'` | flatten | integer | Use FieldName as a path qualifier for FieldType |

* FieldOptions MUST include zero or one instance of each of the options in [Table 3-5](#table-3-5-field-options).  
* All type options ([Table 3-2](#table-3-2-type-options)) included in FieldOptions MUST apply to FieldType as defined in [Table 3-3](#table-3-3-allowed-options). 

#### 3.2.2.1 Multiplicity
The *minc* and *maxc* options specify the minimum and maximum cardinality (number of elements) in a field of an Array, Map, or Record type. Multiplicity, as used in the Unified Modeling Language ([UML](#uml)), is a range of allowed cardinalities:

| minc | maxc | Multiplicity | Description | Keywords |
| ---: | ---: | ---: | :--- | :--- |
| 1 | 1 | 1 | Exactly one instance | Required |
| 0 | 1 | 0..1 | No instances or one instance | Optional |
| 1 | 0 | 1..* | At least one instance | Required, Repeatable |
| 0 | 0 | 0..* | Zero or more instances | Optional, Repeatable |
| m | n | m..n | At least m but no more than n instances | Required, Repeatable if m > 1 |

The default value of both minc and maxc is 1; if neither are specified the field must have exactly one instance of FieldType. If minc is 0, the field is optional. If maxc is 0, the maximum number of elements is unspecified (*).

#### 3.2.2.2 Referenced Field Type
*tfield*

#### 3.2.2.3 Flattened Serialization
*flatten*

### 3.3 Type Simplification
JADN includes several optimizations that make type definitions more compact or that support the
[DRY](#dry) software design principle. These can be removed without affecting
the meaning of a type definition. Removing them simplifies the original definition but creates
additional definitions to support it. This simplifies the code needed to serialize and validate data
instances, and examining the expanded definitions may aid understanding. But expansion can make
specifications more difficult to maintain by introducing redundant data that must be kept in sync.

An optimized specification can be translated into an expanded version that does not include
the following options:

#### Type Definition within fields
A specific type (e.g., an email address) may be defined anonymously within a field of a structure
definition, or it may be defined in a separate named type that can be used in one or more structures.
* Expansion MUST convert all anonymous type definitions to explicit named types and exclude all type options
([Table 3-2](#table-3-2-type-options)) from FieldOptions.
#### Field Multiplicity
Fields may be defined to have multiple values of the same type. Expansion converts each field that can
have more than one value to an explicit ArrayOf type. The minimum and maximum cardinality (minc and maxc)
field options ([Table 3-5](#table-3-5-field-options)) are moved from FieldOptions to the minimum and maximum
length (minv and maxv) TypeOptions of the new ArrayOf type. The only exception is that if minc is 0
(field is optional), it remains in FieldOptions and the new ArrayOf type defaults to a minimum
length of 1.
#### Derived Enumerations
An Enumerated type defined with the *enum* option has fields copied from the type referenced by BaseType
instead of listed in the definition.
* Expansion MUST remove *enum* from Type Options and add fields containing
FieldID, FieldName, and FieldDescription from each field of the referenced type.

A type reference in the form of an Enum() function is converted to the name of an explicit Enumerated
type derived from the referenced type.
* Expansion MUST reference an explicit Enumerated type if it exists, otherwise it MUST create an explicit
Enumerated type. Expansion MUST then replace the type reference with the name of the explicit Enumerated type.

Example:

    Pixel = Map {
        1 red   Integer,
        2 green Integer,
        3 blue  Integer
    }
    Channel = Enumerated(Enum(Pixel)) 
    ChannelMask = ArrayOf(Enum(Pixel))

Expansion replaces the references with:

    Channel = Enumerated {
        1 red,
        2 green,
        3 blue
    }
    ChannelMask = ArrayOf(Channel)

#### MapOf with Enumerated key
A MapOf type where *ktype* is Enumerated is equivalent to a Map.  Expansion removes the MapOf type definition
and creates a Map type with keys from the Enumerated type. This is the complementary operation to derived
enumeration. This expansion can simplify specifications that do not require the more general MapOf type,
and improve robustness by limiting Map keys to a known set.

Example: given an Enumerated type Channel, expansion replaces the following MapOf definition with the explicit Map shown above.

    Pixel = MapOf(Channel, Integer)


# 4 Serialization
Applications may use any internal information representation that exhibits the characteristics defined in [Table 3-1](#table-3-1-jadn-types). Serialization rules define how to represent instances of each type using a specific format. Several serialization formats are defined in this section. In order to be usable with JADN, serialization formats defined elsewhere must:
* Specify an unambiguous serialized representation for each JADN type
* Specify how each option applicable to a type affects serialized values
* Specify any validation requirements defined for that format

## 4.1 JSON Serialization
The following serialization rules are used to represent JADN data types in a human-friendly JSON format.

* When using JSON serialization, instances of JADN types without a format option listed in this section MUST be serialized as:

| JADN Type | JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of [RFC 4648](#rfc4648). |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Enumerated** | JSON **string** |
| **Enumerated** with "id" | JSON **integer** |
| **Choice** | JSON **object** with one member.  Member key is FieldName.   |
| **Choice** with "id" | JSON **object** with one member. Member key is FieldID converted to string. |
| **Array** | JSON **array** of values with types specified by FieldType. Omitted optional values are **null** if before the last specified value, otherwise omitted. |
| **ArrayOf** | JSON **array** of values with type *vtype*, or JSON **null** if *vtype* is Null. |
| **Map** | JSON **object**. Member keys are FieldNames. |
| **Map** with "id" | JSON **object**. Member keys are FieldIDs converted to strings. |
| **MapOf** | JSON **object**, or JSON **null** if *vtype* is Null. Members have key type *ktype* and value type *vtype*. |
| **Record** | Same as **Map**. |

**Format options that affect JSON serialization**
* When using JSON serialization, instances of JADN types with one of the following format options MUST be serialized as:

| Option | JADN Type | JSON Serialization Requirement |
| :--- | :--- | :--- |
| **x** | Binary | JSON **string** containing Base16 (hex) encoding of a binary value as defined in [RFC 4648](#rfc4648) Section 8. Note that the Base16 alphabet does not include lower-case letters. |
| **ipv4-addr** | Binary | JSON **string** containing a "dotted-quad" as specified in [RFC 2673](#rfc2673) Section 3.2. |
| **ipv6-addr** | Binary | JSON **string** containing the text representation of an IPv6 address as specified in [RFC 4291](#rfc4291) Section 2.2. |
| **ipv4-net** | Array | JSON **string** containing the text representation of an IPv4 address range as specified in [RFC 4632](#rfc4632) Section 3.1. |
| **ipv6-net** | Array | JSON **string** containing the text representation of an IPv6 address range as specified in [RFC 4291](#rfc4291) Section 2.3. |

## 4.2 CBOR Serialization
The following serialization rules are used to represent JADN data types in Concise Binary
Object Representation ([CBOR](#rfc7049)) format, where CBOR type #x.y = Major type x, Additional information y.

CBOR type names from Concise Data Definition Language ([CDDL](#cddl)) are shown for reference.

* When using CBOR serialization, instances of JADN types without a format option listed in this section MUST be serialized as:

| JADN Type | CBOR Serialization Requirement |
| :--- | :--- |
| **Binary** | **bstr**: a byte string (#2). |
| **Boolean** | **bool**: a Boolean value (False = #7.20, True = #7.21). |
| **Integer** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Number** |  **float64**: IEEE 754 Double-Precision Float (#7.27). |
| **Null** | **null**: (#7.22) |
| **String** | **tstr**: a text string (#3). |
| **Enumerated** | **int**: an unsigned integer (#0) or negative integer (#1) FieldID. |
| **Choice** | **struct**: a map (#5) containing one pair. The first item is a FieldID, the second item has the corresponding FieldType. |
| **Array** | **record**: an array of values (#4) with types specified by FieldType. Omitted optional values are **null** (#7.22) if before the last specified value, otherwise omitted. |
| **ArrayOf** | **vector**: an array of values (#4) of type *vtype*, or **null** (#7.22) if vtype is Null. |
| **Map** | **struct**: a map (#5) of pairs. In each pair the first item is a FieldID, the second item has the corresponding FieldType. |
| **MapOf** | **table**: a map (#5) of pairs, or **null** if *vtype* is Null. In each pair the first item has type *ktype*, the second item has type *vtype*. |
| **Record** | Same as **Array**. |

**Format options that affect CBOR Serialization**
* When using CBOR serialization, instances of JADN types with one of the following format options MUST be serialized as:

| Option | JADN Type | CBOR Serialization Requirement |
| :--- | :--- | :--- |
| **f16** | Number | **float16**: IEEE 754 Half-Precision Float (#7.25). |
| **f32** | Number | **float32**: IEEE 754 Single-Precision Float (#7.26). |

## 4.3 M-JSON Serialization:
Minimized JSON serialization rules represent JADN data types in a compact format optimized for machine-to-machine communication.  They produce JSON instances identical to [CDDL](#cddl) serialization using the JSON preface defined in CDDL Appendix E.

* When using M-JSON serialization, instances of JADN types MUST be serialized as:

| JADN Type | M-JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Enumerated** | JSON **integer** |
| **Choice** | JSON **object** with one member. Member key is the FieldID converted to string. |
| **Array** | JSON **array** of values with types specified by FieldType. Unspecified values are **null** if before the last specified value, otherwise omitted. |
| **ArrayOf** | JSON **array** of values with type *vtype*, or JSON **null** if *vtype* is Null. |
| **Map** | JSON **object**. Member keys are FieldIDs converted to strings. |
| **MapOf** | JSON **object**, or JSON **null** if *vtype* is Null. Members have key type *ktype* and value type *vtype*. |
| **Record** | Same as **Array**. |

## 4.4 XML Serialization:
* When using XML serialization, instances of JADN types without a format option listed in this section MUST be serialized as:

| JADN Type | XML Serialization Requirement |
| :--- | :--- |
| **Binary** | XML \<Base64Binary\> element with a base64Binary canonical lexical value |
| **Boolean** | XML attribute with the value "true" or "false" |
| **Integer** | |
| **Number** | |
| **Null** | |
| **String** | |
| **Enumerated** | |
| **Choice** | |
| **Array** | |
| **ArrayOf** | |
| **Map** | |
| **MapOf** | |
| **Record** | |

**Format options that affect XML serialization**
* When using XML serialization, instances of JADN types with one of the following format options MUST be serialized as:

| Option | JADN Type | XML Serialization Requirement |
| :--- | :--- | :--- |
| **x** | Binary | XML \<HexBinary\> element with a hexBinary canonical lexical value. |

# 5 JADN Schemas
A JADN module consists of a set of type definitions, plus metadata related to the module.
JADN modules can be developed independently without knowledge of or coordination with each other,
and types defined in one module can be used in others.

A JADN schema defines the full interface to an application or service, and consists of definitions
contained in one or more modules. A schema is constructed by starting with the base module for an
interface and recursively incorporating definitions from each module listed as an import.

## 5.1 Type Definition Styles
[Section 3.1](#31-type-definitions) specifies the authoritative format of JADN type definitions.
Although JSON data is unambiguous and machine-readable, it is not an ideal presentation format.
This section describes two presentation styles for JADN type definitions that ...

### 5.1.1 Table Style
```
+----------+------------+----------+
| TypeName | TypeString | TypeDesc |
+----------+------------+----------+
```
followed by
```
+---------+-----------+-------------+-----------+
| FieldID | FieldName | FieldString | FieldDesc |
+---------+-----------+-------------+-----------+
or
+---------+-------------+-----------------------+
| FieldID | FieldString | FieldName:: FieldDesc |
+---------+-------------+-----------------------+
```

### 5.1.2 IDL Style


## 5.2 Meta Information

A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)
* option format (id/value string for JSON, Multiplicity ... for tables)

# 6 Data Model Generation
A JADN schema can be combined with a set of serialization rules to produce a DM, a schema applicable to the serialized data format.

# 7 Operational Considerations
* Serialization (bulk vs pull)
* Validation (integrated with serialization, separate)
* Schema expansion (unsweetening) - optional
* Localization
* Schema embedding - self-describing data
* Bridging
* Tabular data (not too many optional columns, sort fields by required/optional.  Tuples.)
-------

# 8 Security Considerations
This document presents a language for expressing the information needs of communicating applications, and rules for generating data structures to satisfy those needs.  As such, it does not inherently introduce security issues, although protocol specifications based on JADN naturally need security analysis when defined. Such specifications need to follow the guidelines in [RFC 3552](#rfc3552).

Additional security considerations applicable to JADN-based specifications: 
* The JADN language could cause confusion in a way that results in security issues. Clarity and unambiguity of this specification could always be improved through operational experience and developer feedback.
* Where a JADN data validator is part of a system, the security of the system benefits from automatic data validation but depends on both the specificity of the JADN specification and the correctness of the validation implementation.  Tightening the specification (e.g., by defining upper bounds and other value constraints) and testing the validator against unreasonable data instances can address both concerns.

Security and size efficiency are the primary reasons for creating an information model. Enumerating strings and map keys means defining the information content of those values, which greatly reduces opportunities for exploitation.  A firewall with a security policy of "Allow these specific things I understand, plus everything I don't understand" is less secure than a firewall that allows only things that it understands. The "Must-Ignore" policy of [RFC 7493](#rfc7493) is in direct conflict with information modeling's "Must-Understand" policy, which accommodates new protocol elements by adding them to the IM's lists of things that are understood.

Writers of JADN specifications are strongly encouraged to value simplicity and transparency of the specification over complexity. Although JADN makes it easier to both define and understand complex specifications, complexity that is not essential to satisfying operational requirements is itself a security concern.

-------

# 9 Conformance

(Note: The [OASIS TC Process](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsConfClause) requires that a specification approved by the TC at the Committee Specification Public Review Draft, Committee Specification or OASIS Standard level must include a separate section, listing a set of numbered conformance clauses, to which any implementation of the specification must adhere in order to claim conformance to the specification (or any optional portion thereof). This is done by listing the conformance clauses here.
For the definition of "conformance clause," see [OASIS Defined Terms](https://www.oasis-open.org/policies-guidelines/oasis-defined-terms-2017-05-26#dConformanceClause).

See "Guidelines to Writing Conformance Clauses":  
http://docs.oasis-open.org/templates/TCHandbook/ConformanceGuidelines.html.

Remove this note before submitting for publication.)

Conformance targets:

* JADN Schema Translator
    * Validate type definitions per Sections 3.1 and 3.2.
    * Perform type simplification operations per Section 3.3.
    * Translate JSON definitions to Table and IDL formats per Section 5.1.
    * Merge schema modules per Section 5.2.
* JADN Reverse Schema Translator
    * Translate Table and IDL definitions to JSON format per Section 5.1.
* JADN Concrete Schema Generator
    * Generate a schema in a format-specific language per serialization rules in Section 4.x.
    Conformance testing requires JADN validator and format-specific validator to agree on all
    good and bad data instances.
* JADN Encoder/Decoder
    * Validate type definition correctness per Sections 3.1 and 3.2.
    * Perform type simplification operations per Section 3.3.
    * Validate API values against type definitions per Sections 3.1 and 3.2.
    * Encode and decode data instances per serialization rules for formats \<X\> and \<Y\> in Section 4.x. 
    Conformance testing requires the implementation under test to support any two serialization formats.

-------

# Appendix A. Acknowledgments

The following individuals have participated in the creation of this specification and are gratefully acknowledged:

**OpenC2 TC Members:**

| First Name | Last Name | Company |
| :--- | :--- | :--- |

-------

# Appendix B. Revision History
| Revision | Date | Editor | Changes Made |
| :--- | :--- | :--- | :--- |
| jadn-v1.0-wd01 | 2019-03-01 | David Kemp | Initial working draft |

# Appendix C. Schema for JADN specifications
Used to validate a JADN specification.  In JADN, JSON Schema, and CDDL formats

# Appendix D. Conformance Tests
Specifications including correct and incorrect definitions used to check implementation conformance.

# Appendix E. Examples


