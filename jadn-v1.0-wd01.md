
![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v2.0.jpg)
-------

# Specification for JSON Abstract Data Notation Version 1.0

## Working Draft 01

## 31 March 2019

### Technical Committee:
* [OASIS Open Command and Control (OpenC2) TC](https://www.oasis-open.org/committees/openc2/)

### Chairs:
* Joe Brule (jmbrule@radium.ncsc.mil), [National Security Agency](https://www.nsa.gov/)
* Duncan Sparrell (duncan@sfractal.com), [sFractal Consulting LLC](http://www.sfractal.com/)

### Editor:
* David Kemp (dkemp@mobility-challenge.com), [National Security Agency](https://www.nsa.gov/)

### Additional artifacts:
This prose specification is one component of a Work Product that also includes:

* JADN Schema for JADN specifications
* JSON Schema for JADN specifications
* CDDL Schema for JADN specifications

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

The keyword "iff" is interpreted to mean "if and only if".  A requirement "X MUST be considered valid iff Y" means that an implementation does not conform unless it evaluates every otherwise valid instance of X for which Y is true as valid, and every instance of X for which Y is false as invalid.

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
###### [RFC5952]
Kawamura S., Kawashima M., "A Recommendation for IPv6 Address Text Representation", RFC 5952, August 2010, http://www.rfc-editor.org/info/rfc5952.
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

\* *Note: all references to information in this document assume uniform distribution over all possible values.*

**Information Modeling**

JADN is based on the [CBOR](#rfc7049) data model ([JSON](#rfc8259) types plus integers, special numbers, and byte strings), but has an
information-centric focus:

| Data-centric | Information-centric |
| --- | --- |
| A data definition language is designed around specific data formats. | An information modeling language is designed to express application needs. |
| JSON Schema defines integer as a value constraint on the JSON number type: "integer matches any number with a zero fractional part". | Integer and Number first-class types exist regardless of data representation. |
| CDDL says: "While CBOR map and array are only two representation formats, they are used to specify four loosely-distinguishable styles of composition". | First-class types are based on five distinct composition styles.  Each type can be represented in multiple data formats. |
| No table composition style is defined. | Tables are a fundamental way of organizing information. The Record first class type holds tabular information that can be represented as both arrays and maps in multiple data formats. |
| Data-centric design is often Anglocentric, embedding English-language identifiers in protocol data. | Information-centric design encourages definition of natural-language-agnostic protocols while supporting localized identifiers within applications. |

**Implementation**

Two general approaches can be used to implement IM-based protocol specifications:
1) Translate the IM to a data-format-specific schema language such [Relax-NG](#relaxng), [JSON Schema](#jsonschema), [Protobuf](#proto), or [CDDL](#cddl), then use format-specific serialization and validation libraries to process data in the selected format. Applications use data objects specific to each serialization format.
2) Use the IM directly as a format-independent schema language, using IM serialization and validation libraries to process data without separate schema generation or code generation steps. Applications use the same IM-specified data objects regardless of serialization format.

# 3 JADN Types
JADN first-class types are defined in terms of their characteristics:

###### Table 3-1. JADN Types

| JADN Type | Definition |
| :--- | :--- |
| **Primitive** |   |
| Binary | A sequence of octets.  Length is the number of octets. |
| Boolean | An element with one of two values: true or false. |
| Integer | A whole number. |
| Number | A real number. |
| Null | An unspecified or non-existent value. |
| String | A sequence of characters, each of which has a Unicode codepoint.  Length is the number of characters. |
| **Structure** |   |
| Enumerated | One value selected from a set of named or unnamed integers. |
| Choice | One key and value selected from a set of named or unnamed fields. The key has an id and name or label, and is mapped to a type. |
| Array | An ordered list of unnamed fields with positionally-defined semantics. Each field has a position, label, and type. Corresponds to CDDL *record*. |
| ArrayOf(*vtype*) | An ordered list of fields with the same semantics. Each field has a position and type *vtype*. Corresponds to CDDL *vector*. |
| Map | An unordered map from a set of specified keys to values with semantics bound to each key. Each key has an id and name or label, and is mapped to a type. Corresponds to CDDL *struct*. |
| MapOf(*ktype*, *vtype*) | An unordered map from a set of keys to values with the same semantics. Each key has key type *ktype*, and is mapped to value type *vtype*. Represents a map with keys that are either enumerated or are members of a well-defined category. Corresponds to CDDL *table*. |
| Record | An ordered map from a list of keys with positions to values with positionally-defined semantics. Each key has a position and name, and is mapped to a type. Represents a row in a spreadsheet or database table. CDDL does not have a corresponding composition style. |

## 3.1 Type Definitions
JADN type definitions have a regular structure designed to be easily describable, easily processed, and extensible. Every definition creates a *Defined type* that has four elements, plus for some types, a list of fields:

1. **TypeName:** the name of the type being defined
2. **BaseType:** the JADN type ([Table 3-1](#table-3-1-jadn-types)) of the type being defined, or the name of a Defined type
3. **TypeOptions:** an array of zero or more **TypeOption** applicable to the type being defined
4. **TypeDescription:** a non-normative comment
5. **Fields:** an array of one or more field definitions, if applicable to BaseType

* If BaseType is a Primitive type, ArrayOf, MapOf, or a Defined type, the type definition MUST NOT include Fields:
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
4. **FieldOptions:** an array of zero or more **FieldOption** ([Table 3-4](#table-3-4-field-options)) or **TypeOption** ([Table 3-2](#table-3-2-type-options)) applicable to the field
5. **FieldDescription:** a non-normative comment
```
[TypeName, BaseType, [TypeOption, ...], TypeDescription, [
    [FieldID, FieldName, FieldType, [FieldOption, TypeOption, ...], FieldDescription],
    ...
]]
```

JADN does not restrict the format of TypeName and FieldName, but naming requirements are needed in order to validate JADN specifications. JADN-based protocol specifications MAY define their own name format requirements.  
* Specifications that do not define an alternate name format MUST use the default format defined in Figure 3-1 using [ABNF](#rfc5234).

```
; Name Format Definitions
TypeName   = UC *31("-" / UC / LC / DIGIT / Sys)   ; e.g., Color-Values, length = 1-32 characters
FieldName  = LC *31("_" / UC / LC / DIGIT)         ; e.g., color_values, length = 1-32 characters
FieldSep   = "/"      ; 'SOLIDUS' (U+002F), Path separator reserved for qualified names, not allowed in FieldName
Sys        = "$"      ; 'DOLLAR SIGN' (U+0024), Reserved for tool-generated type names, e.g., $Colors.

; Constants
UC         = %x41-5A  ; A-Z
LC         = %x61-7A  ; a-z
DIGIT      = %x30-39  ; 0-9
```
###### Figure 3-1: JADN Default Name Syntax in ABNF

```
TypeName:  ^([A-Z]([-A-Za-z0-9]|\$){,31})$
FieldName: ^([a-z][_A-Za-z0-9]{,31})$
```
###### Figure 3-2: JADN Default Name Syntax Regular Expressions

* TypeName MUST NOT be a JADN type ([Table 3-1](#table-3-1-jadn-types)).  
* FieldID and FieldName values MUST be unique within a type definition.  
* If BaseType is Array or Record, FieldID MUST be the position of the field within the type, numbered consecutively starting at 1.

If BaseType is Enumerated, Choice, or Map, FieldID MAY be any nonconflicting integer tag.  
* FieldType MUST be a Primitive type, ArrayOf, MapOf, or a Derived Enumeration ([Section 3.2.1.4](#3214-derived-enumeration)).

**Type Definition Formats**

JADN type definitions are themselves information objects that can be represented in many ways. [Section 5](#5-jadn-schema-formats) defines several equivalent representation formats. The [Protobuf](#proto) introduction has an example Person structure with three fields, the third of which is optional. The equivalent JADN definitions are:

**JADN definition of Person in [JSON](#rfc8259) format:**
```
["Person", "Record", [], "", [
    [1, "name", "String", [], ""],
    [2, "id", "Integer", [], ""],
    [3, "email", "String", ["[0"], ""]
]]
```
**JADN definition of Person in [GFM](#gfm) table format:**

  *Type: Person (Record)*

|  ID  |    Name   |   Type  |   #  | Description |
| ---: | --------- | ------- | ---: | ----------- |
|   1  | **name**  | String  |    1 |             |
|   2  | **id**    | Integer |    1 |             |
|   3  | **email** | String  | 0..1 |             |

**JADN definition of Person in a [Thrift](#thrift)-like IDL format:**
```
record Person {
  1: string name,
  2: int id,
  3: optional string email
}
```
These examples represent identical IM definitions, but the JSON data is structured as defined in this section and can be read unambiguously by applications with no language-specific parsing code. JADN definitions in JSON format are considered authoritative over other formats; specifications that include JADN definitions in another format SHOULD also make the same definitions available in JSON format.

## 3.2 Options
This section defines the mechanism used to support a varied set of information needs within the strictly regular structure of [Section 3.1](#31-type-definitions). New requirements can be accommodated by defining new options without modifying that structure.

### 3.2.1 Type Options
Type options apply to the type definition as a whole. Structural options are intrinsic elements of the types defined in ([Table 3-1](#table-3-1-jadn-types)). Validation options are optional; if present they constrain which data values are instances of the defined type.

###### Table 3-2. Type Options

| ID | Label | Type | Definition |
| --- | --- | --- | --- |
|  **Structural** | | | |
| 0x3d `'='` | id | none | If present, FieldName is a suggested label rather than an immutable name |
| 0x2a `'*'` | vtype | string | Value type for ArrayOf and MapOf |
| 0x2b `'+'` | ktype | string | Key type for MapOf |
| 0x24 `'$'` | enum | string | Enumerated type derived from a defined Array, Choice, Map or Record type |
| **Validation** | | | |
| 0x40 `'@'` | format | string | Semantic validation keyword from [Section 3.2.1.3](#3213-semantic-validation-keywords) |
| 0x2f `'/'` | sopt | string | Serialization option from [Section 4](#4-serialization), may also include semantic validation |
| 0x25 `'%'` | pattern | string | Regular expression used to validate a String type ([Section 3.2.1.4](#3214-patterns) |
| 0x7b `'{'` | minv | integer | Minimum numeric value, octet or character count, or element count |
| 0x7d `'}'` | maxv | integer | Maximum numeric value, octet or character count, or element count |
| 0x21 `'!'` | default | string | Default value for an instance of this type |

* If BaseType is ArrayOf, TypeOptions MUST include a *vtype* option.
* If BaseType is MapOf, TypeOptions MUST include *ktype* and *vtype* options.
* TypeOptions MUST contain zero or one instance of each type option except 0x2f (serialization option).
* TypeOptions MUST contain zero or one serialization option defined for each serialization format.
* TypeOptions MUST contain only TypeOptions allowed for BaseType as shown in Table 3-3.

###### Table 3-3. Allowed Options

| BaseType | Allowed Options |
| :--- | :--- |
| Binary | minv, maxv, format, sopt |
| Boolean | |
| Integer | minv, maxv, format, sopt |
| Number | minv, maxv, format, sopt |
| Null | |
| String | minv, maxv, format, sopt, pattern |
| Enumerated | id |
| Choice | id |
| Array | format, sopt |
| ArrayOf | vtype, minv, maxv |
| Map | id, minv, maxv |
| MapOf | ktype, vtype, minv, maxv |
| Record | |
| Defined | enum |

* If BaseType is not a JADN type, TypeOptions MUST NOT contain any option other than *enum*.
* If TypeOptions is *enum*, the definition named by BaseType MUST have a BaseType of Choice, Array, Map, or Record.
* If TypeOptions is *vtype* or *ktype*, ...

#### 3.2.1.1 Id

The Enumerated, Choice, and Map types have named and unnamed variants. Presence of the *id* option in a type definition indicates that the type is unnamed. The Record type is always named and has no *id* option; the Array type is its unnamed equivalent.

* In named types, FieldName is a defined name that is included in the semantics of the type, must be populated in the type definition, may appear in serialized data, and cannot be changed without affecting interoperability.
* In unnamed types, FieldName is a suggested label that is not included in the semantics of the type, may be empty in the type definition, never appears in serialized data, and may be freely customized without affecting interoperability.

For example a list of HTTP status codes could include the field [403, "Forbidden"].  If the Enumerated type definition does not include the *id* option, serialization rules determine whether FieldID or FieldName is used in protocol data, and the name "Forbidden" cannot be changed. With the *id* option the FieldID 403 is always used in protocol data, but the label "Forbidden" may be displayed in messages or user interfaces, as could customized labels such as "NotAllowed", "Verboten", or "Interdit".

#### 3.2.1.2 Value Type

The *vtype* option specifies the type of each field in an ArrayOf or MapOf type. It may be any JADN type or Defined type.
* An ArrayOf or MapOf instance MUST be considered valid iff each of its elements is an instance of *vtype*.

#### 3.2.1.3 Key Type
The *ktype* option specifies the type of each key in a MapOf type. 
* *ktype* MUST be a Defined type, either an enumeration or a type with constraints that specify a fixed subset of values that belong to a category.
* A MapOf instance MUST be considered valid iff each of its keys is an instance of *ktype*.

#### 3.2.1.4 Derived Enumeration
The *enum* option creates an enumeration derived from a referenced Array, Choice, Map or Record type. (See [Section 3.2.3](#323-syntactic-sugar)). The referenced type is specified by either the BaseType element or the ktype/vtype options of a type definition. This is the only kind of type definition where BaseType is not a JADN type.

#### 3.2.1.5 Format
*format*

*sopt - Serialization options may include value constraints applicable to all data formats.*
* IM value is an IPv4 address as defined in [RFC 791](#rfc791).
* IM value is an IPv6 address as defined in [RFC 8200](#rfc8200). 
* IM value is an IPv4 address and a prefix length as specified in Section 3.1 of [RFC 4632](#rfc4632).
* IM value is an IPv6 address and a prefix length as specified in Section 2.3 of [RFC 4291](#rfc4291).

#### 3.2.1.6 Pattern
The *pattern* option specifies a regular expression used to validate a String instance.
* The *pattern* option SHOULD conform to the Pattern grammar of [ECMAScript](#es9) Section 21.2.
* A String instance MUST be considered valid iff it matches the regular expression specified by *pattern*.

#### 3.2.1.7 Size and Value Constraints
The *minv* and *maxv* options specify size or value limits.
* A Binary instance MUST be considered valid iff its number of bytes is at least *minv* and no more than *maxv*.
* A String instance MUST be considered valid iff its number of characters is at least *minv* and no more than *maxv*.
* An Integer or Number instance MUST be considered valid iff its value is at least *minv* and no more than *maxv*.
* An ArrayOf, Map, or MapOf instance MUST be considered valid iff it contains at least *minv* and no more than *maxv* elements.

#### 3.2.1.8 Default Value
The *default* option is reserved for future use. It is intended to specify the value a receiving application uses for an optional field if an instance does not include its value.

### 3.2.2 Field Options
Field options apply to each field within a type definition. Each option in Table 3-4 is a structural element of the type definition.

###### Table 3-4. Field Options

| ID | Label | Type | Definition |
| --- | --- | --- | --- |
| 0x5b `'['` | minc | integer | Minimum cardinality |
| 0x5d `']'` | maxc | integer | Maximum cardinality |
| 0x26 `'&'` | tfield | enum | Field that specifies the type of this field |
| 0x3c `'<'` | flatten | integer | Use FieldName as a path qualifier for FieldType |

* FieldOptions MUST include zero or one instance of each of the options in [Table 3-4](#table-3-4-field-options).  
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

### 3.2.3 Syntactic Sugar
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
Expansion converts all anonymous type definitions to explicit named types and excludes all type options
([Table 3-2](#table-3-2-type-options)) from FieldOptions.
#### Field Multiplicity
Fields may be defined to have multiple values of the same type. Expansion converts each field that can
have more than one value to an explicit ArrayOf type. The minimum and maximum cardinality (minc and maxc)
field options ([Table 3-4](#table-3-4-field-options)) are moved from FieldOptions to the minimum and maximum
length (minv and maxv) TypeOptions of the new ArrayOf type. The only exception is that if minc is 0
(field is optional), it remains in FieldOptions and the new ArrayOf type defaults to a minimum
length of 1.
#### Derived Enumerations
A type defined with the *enum* option generates an anonymous Enumerated type whose fields are the ID and Name values
of the the referenced type.  Expansion explicitly creates a new Enumerated type definition and removes the *enum* option.
#### MapOf with Enumerated key
A MapOf type where *ktype* is Enumerated is equivalent to a Map.  Expansion removes the MapOf type definition
ahd creates a Map type with keys from the Enumerated type. This is the complementary operation to derived
enumeration. This expansion can simplify specifications that do not require the more general MapOf type,
and improve robustness by limiting Map keys to a known set. 

# 4 Serialization

Applications may use any internal information representation that exhibits the characteristics defined in [Table 3-1](#table-3-1-jadn-types). Serialization rules define how to represent instances of each type using a specific format. Several serialization formats are defined in this section. In order to be usable with JADN, serialization formats defined elsewhere must:
* Specify an unambiguous serialized representation for each JADN type
* Specify how each option applicable to a type affects serialized values
* Specify any validation requirements defined for that format

## 4.1 JSON Serialization

The following JSON serialization rules are used to represent JADN data types in a human-friendly format.

* 4.1-1: When using JSON serialization, instances of JADN types without a serialization option defined in this section MUST be serialized as:

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

**JSON Serialization Options**

Regardless of serialization:
* A JADN type definition MUST NOT contain more than one of the following options.
* A JADN type definition MUST NOT contain a serialization option not applicable to its type.
* API values MUST satisfy the validation requirements associated with a serialization option.

When using JSON serialization:
* instances of JADN types with one of the following options MUST be serialized as:

| Option | JADN Type | JSON Serialization Requirement | Validation Requirement |
| :--- | :--- | :--- | :--- |
| **/x** | Binary | JSON **string** containing Base16 (hex) encoding of a binary value as defined in Section 8 of [RFC 4648](#rfc4648). Note that the Base16 alphabet does not include lower-case letters. | None |
| **/ipv4-addr** | Binary | JSON **string** containing a "dotted-quad" as specified in Section 3.2 of [RFC 2673](#rfc2673). | Address as specified in Section 3.1 of [RFC 791](#rfc791) |
| **/ipv6-addr** | Binary | JSON **string** containing the text representation of an IPv6 address as specified in Section 4 of [RFC 5952](#rfc5952). | Address as specified in Section 3 of [RFC 8200](#rfc8200) |
| **/ipv4-net** | Array | JSON **string** containing the text representation of an IPv4 address range as specified in Section 3.1 of [RFC 4632](#rfc4632). | Two components as specified in [RFC 4632](#rfc4632): Binary IPv4 address and Integer prefix length. |
| **/ipv6-net** | Array | JSON **string** containing the text representation of an IPv6 address range as specified in Section 2.3 of [RFC 4291](#rfc4291). | Two components as specified in [RFC 4291](#rfc4291): Binary IPv6 address and Integer prefix length. |

## 4.2 CBOR Serialization

The following serialization rules are used to represent JADN data types in Concise Binary
Object Representation ([CBOR](#rfc7049)) format, where CBOR type #x.y = Major type x, Additional information y.
* The id TypeOption does not affect serialized values.

CBOR type names from Concise Data Definition Language ([CDDL](#cddl)) are shown for reference.

* When using CBOR serialization, instances of JADN types without a serialization option defined in this section MUST be serialized as:

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

**CBOR Serialization Options**

Regardless of serialization:
* A JADN type definition MUST NOT contain more than one of the following options.
* A JADN type definition MUST NOT contain a serialization option not applicable to its type.
* API values MUST satisfy the validation requirements associated with a serialization option.

When using CBOR serialization:
* Instances of JADN types with one of the following options MUST be serialized as:

| Option | JADN Type | CBOR Serialization Requirement | Validation Requirement |
| :--- | :--- | :--- | :--- |
| **/f16** | Number | **float16**: IEEE 754 Half-Precision Float (#7.25). | None |
| **/f32** | Number | **float32**: IEEE 754 Single-Precision Float (#7.26). | None |

## 4.3 M-JSON Serialization:

Minimized JSON serialization rules represent JADN data types in a compact format optimized for machine-to-machine communication.  They produce JSON instances identical to [CDDL](#cddl) serialization using the JSON preface defined in CDDL Appendix E.
* Serialization and id TypeOptions do not affect serialized values.

When using M-JSON serialization:
* Instances of JADN types MUST be serialized as:

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

*Editor's Note: Define XML rules for elements and attributes*

When using XML serialization:
* Instances of JADN types MUST be serialized as:

| JADN Type | XML Serialization Requirement |
| :--- | :--- |
| **Binary** |  |
| **Boolean** | |
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

# 5 JADN Schema Formats
A JADN schema is:
* a collection of type definitions
* meta-information related to the schema
## 5.1 Type Definitions
### 5.1.1 JSON Format
The structure of type definitions in JSON format is specified in [Section 3.1](#31-type-definitions).

### 5.1.2 Table Format
### 5.1.3 JADN IDL Format

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

Writers of JADN specifications are strongly encouraged to value simplicity and transparency of the specification over complexity. Although JADN makes it easier to both define and understand complex specifications, complexity that is not essential to satisfying operational requirements is itself a security concern.

-------

# 9 Conformance

(Note: The [OASIS TC Process](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsConfClause) requires that a specification approved by the TC at the Committee Specification Public Review Draft, Committee Specification or OASIS Standard level must include a separate section, listing a set of numbered conformance clauses, to which any implementation of the specification must adhere in order to claim conformance to the specification (or any optional portion thereof). This is done by listing the conformance clauses here.
For the definition of "conformance clause," see [OASIS Defined Terms](https://www.oasis-open.org/policies-guidelines/oasis-defined-terms-2017-05-26#dConformanceClause).

See "Guidelines to Writing Conformance Clauses":  
http://docs.oasis-open.org/templates/TCHandbook/ConformanceGuidelines.html.

Remove this note before submitting for publication.)

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

# Appendix C. JADN Information Model
JADN IM validates any JADN schema in any serialized format
# Appendix D. JSON-Schema Data Model for JADN
JSON Schema generated from the JADN IM, validates any JADN schema in JSON format
# Appendix E. CDDL Data Model for JADN
CDDL generated from the JADN IM, validates any JADN schema in CBOR format

