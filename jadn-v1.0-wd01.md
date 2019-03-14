
![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v2.0.jpg)
-------

# Specification for JSON Abstract Data Notation Version 1.0

## Working Draft 01

## 01 March 2019

### Technical Committee:
* [OASIS Open Command and Control (OpenC2) TC](https://www.oasis-open.org/committees/openc2/)

### Chairs:
* Joe Brule (jmbrule@radium.ncsc.mil), [National Security Agency](https://www.nsa.gov/)
* Duncan Sparrell (duncan@sfractal.com), [sFractal Consulting LLC](http://www.sfractal.com/)

### Editor:
* David Kemp (dkemp@mobility-challenge.com), [National Security Agency](https://www.nsa.gov/)

### Additional artifacts:
This prose specification is one component of a Work Product that also includes:
* *Editor's Note: list JADN Schemas: (JSON, CDDL)*

### Related work:
[Avro](#avro) is a dynamic data serialization system. Like JADN, Avro does not require code generation and supports embedding of schema information to produce self-describing data. Unlike JADN, Avro has its own data format and cannot be used with JSON or CBOR data.

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

*Editors Notes:*

*Capabilities developed in XML, various means to move to JSON, then CBOR.*

*Standards are created using data definition tables with a goal of being agnostic of transfer format, but no well-defined mechanism exists for achieving that goal. JADN defines a table structure that translates completely and unambiguously to a machine-usable schema. The schema serves as "byte code" that can be transferred between applications and interpreted to validate application data. It can be embedded to produce self-describing data.*

*Numerous data definition languages are in use. JADN doesn't replace any of them, but serves as a Rosetta stone to facilitate translation among them.*

## 1.1 IPR Policy
This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode) Mode of the [OASIS IPR Policy](https://www.oasis-open.org/policies-guidelines/ipr), the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page ([https://www.oasis-open.org/committees/openc2/ipr.php](https://www.oasis-open.org/committees/openc2/ipr.php)).

## 1.2 Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [[RFC2119](#rfc2119)] and [[RFC8174](#rfc8174)] when, and only when, they appear in all capitals, as shown here.

## 1.3 Normative References
###### [RFC791]

###### [RFC2119]
Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997, http://www.rfc-editor.org/info/rfc2119.
###### [RFC2673]

###### [RFC4291]

###### [RFC4632]

###### [RFC4648]

###### [RFC5952]

###### [RFC7049]
*"Concise Binary Object Representation (CBOR)"*, https://tools.ietf.org/html/rfc7049

###### [RFC8174]
Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174, May 2017, http://www.rfc-editor.org/info/rfc8174.

###### [RFC8200]

## 1.4 Non-Normative References
###### [AVRO]
*"Apache Avro Documentation"*, https://avro.apache.org/docs/current/

###### [CDDL]
*"Concise Data Definition Language"*, https://tools.ietf.org/html/draft-ietf-cbor-cddl-07

###### [DRY]
*"Don't Repeat Yourself"*, https://en.wikipedia.org/wiki/Don%27t_repeat_yourself

###### [GFM]
*"GitHub Flavored Markdown"*, https://github.github.com/gfm/

###### [JSONSCHEMA]
*"JSON Schema Validation"*, https://tools.ietf.org/html/draft-handrews-json-schema-validation-01

###### [MDA]
*"The Fast Guide to Model Driven Architecture"*, https://www.omg.org/mda/mda_files/Cephas_MDA_Fast_Guide.pdf

###### [PROTO]
*"Protocol Buffers"*, https://developers.google.com/protocol-buffers/

###### [RELAXNG]
*"RELAX NG"*, https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=relax-ng

###### [RFC2673]
*"Binary Labels in the Domain Name System"*, https://tools.ietf.org/html/rfc2673

###### [RFC3444]
*"On the Difference between Information Models and Data Models"*, https://tools.ietf.org/html/rfc3444

###### [RFC3552]
Rescorla, E. and B. Korver, "Guidelines for Writing RFC Text on Security Considerations", BCP 72, RFC 3552, DOI 10.17487/RFC3552, July 2003, https://www.rfc-editor.org/info/rfc3552.

###### [THRIFT]
*"Writing a .thrift file"*, https://thrift-tutorial.readthedocs.io/en/latest/thrift-file.html

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
data used for purposes such as text conversion, delimiting, and framing contains no entropy because it is known a priori.
If the serialization is non-canonical, any additional entropy introduced during serialization
(e.g., whitespace, leading zeroes, reordering, case-insensitive capitalization) is discarded on deserialization.

For example, an IPv4 address contains 32 bits of information. But different data may be used to
represent the same information:
* IPv4 dotted-quad contained in a JSON string: "192.168.141.240" (17 bytes / 136 bits).
* Hex value contained in a JSON string: "C0A88DF0" (10 bytes / 80 bits)
* CBOR byte string: 0x44c0a88df0 (5 bytes / 40 bits).

**Information Modeling**

JADN is based on the [CBOR](#rfc7049) data model (JSON types plus integers, special numbers, and byte strings), but has an
information-centric focus:

| Data-centric | Information-centric |
| --- | --- |
| A data definition language is designed around specific data formats. | An information modeling language is designed to express application needs. |
| JSON Schema defines integer as a value constraint on the JSON number type: "integer matches any number with a zero fractional part". | Integer and Number first-class types exist regardless of data representation. |
| CDDL says: "While CBOR map and array are only two representation formats, they are used to specify four loosely-distinguishable styles of composition". | First-class types are based on five distinct composition styles.  Each type can be represented in multiple data formats. |
| No table composition style is defined. | Tables are a fundamental way of organizing information. The Record first class type holds tabular information that can be represented as both arrays and maps in multiple data formats. |
| Data-centric design is often Anglocentric, embedding English-language identifiers in protocol data. | Information-centric design encourages definition of natural-language-agnostic protocols while supporting localization of identifiers within applications. |

**Implementation**

Two general approaches can be used to implement IM-based specifications:
1) Translate the IM to a format-specific schema language such [Relax-NG](#relaxng), [JSON Schema](#jsonschema) or [CDDL](#cddl), then use existing serialization and validation libraries to process data in the selected format.
2) Use the IM directly as a format-independent schema language, using IM serialization and validation libraries to process data without separate schema-generation or code-generation steps. 

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
| Record | An ordered map from a list of keys with positions to values with positionally-defined semantics. Each key has a position and name, and is mapped to a type. Represents a row in a spreadsheet or database table. CDDL has no corresponding composition style. |

## 3.1 Type Definitions
JADN type definitions have a simple, regular structure designed to be easily describable, easily processed, and extensible. Every JADN type definition has four elements, plus for some types, a list of fields:

1. **TypeName:** the name of the type being defined
2. **BaseType:** the JADN type ([Table 3-1](#table-3-1-jadn-types)) of the type being defined
3. **TypeOptions:** an array of zero or more options applicable to the type being defined
4. **TypeDescription:** a non-normative comment
5. **Fields:** an array of one or more field definitions, if applicable to BaseType

Primitive, ArrayOf, and MapOf base types MUST have no field definitions.  
The ArrayOf base type MUST have a *vtype* option ([Section 3.2.1.2](#3212-vtype-and-ktype)).  
The MapOf base type MUST have a *ktype* option and a *vtype* option.

Field definitions for the Enumerated base type MUST have three elements:
1. **FieldID:** the integer identifier of the field
2. **FieldName:** the name or label of the field
3. **FieldDescription:** a non-normative comment

Field definitions for the Array, Choice, Map, and Record base types MUST have five elements:
1. **FieldID:** the integer identifier of the field
2. **FieldName:** the name or label of the field
3. **FieldType:** the type of the field
4. **FieldOptions:** an array of zero or more options applicable to the field
5. **FieldDescription:** a non-normative comment

FieldID and FieldName values MUST be unique within a type definition.  
In Array and Record base types, FieldID MUST be the position of the field within the type, numbered consecutively starting at 1.  
In Enumerated, Choice and Map base types, FieldID may be any nonconflicting integer tag.

JADN type definitions are themselves information objects that can be represented in many ways. [Section 5](#5-jadn-schema-formats) defines several representation formats, but for concreteness this example (from [Protobuf](#proto)) defines a Record type called Person with three fields, the third of which is optional:

JADN definition of Person in JSON format:
```
["Person", "Record", [], "", [
  [1, "name", "String", [], ""],
  [2, "id", "Integer", [], ""],
  [3, "email", "String", ["[0"], ""]
]]
```
JADN definition of Person in [GFM Markdown](#gfm) table format:

***Type: Person (Record)***

| ID | Name | Type | # | Description |
| ---: | --- | --- | ---: | --- |
| 1 | **name** | String | 1 | |
| 2 | **id** | Integer | 1 | |
| 3 | **email** | String | 0..1 | |

JADN definition of Person in an IDL format similar to [Apache Thrift](#thrift):
```
record Person {
  1: string name,
  2: integer id,
  3: optional string email,
}
```
Of these examples, only JSON is data that can be read unambiguously by applications with no format-specific parsing code. For that reason, JADN definitions in JSON format are considered authoritative over other formats. Specifications that include JADN definitions in a non-data format SHOULD also make available the same definitions in JSON format.

## 3.2 Options
This section defines the mechanism used to support a varied set of information needs within the strictly regular structure of [Section 3.1](#31-type-definitions). New requirements are accommodated by defining new options without needing to update the structure of type definitions.

### 3.2.1 Type Options
Type options apply to the type definition as a whole. Structural options are intrinsic elements of the types defined in ([Table 3-1](#table-3-1-jadn-types)). Validation options are optional; if present they constrain which values if a type are considered valid.

###### Table 3-2. Type Options

| ID | Label | Type | Applies To | Definition |
| --- | --- | --- | --- | --- |
| - | - | - | - | **Structural Options** |
| 0x3d `'='` | id | none | Enumerated, Choice, Map | If present, FieldName is a suggested label rather than a defined name |
| 0x2a `'*'` | vtype | string | ArrayOf, MapOf | Value type for ArrayOf/MapOf, or Enumerated value derived from Choice/Map/Array/Record |
| 0x2b `'+'` | ktype | string | MapOf | Key type for MapOf |
| - | - | - | - | **Validation Options** |
| 0x40 `'@'` | format | string | Any | Semantic validation keyword from [Section 3.2.1.3](#3213-semantic-validation-keywords) |
| 0x2f `'/'` | sopt | string | Any | Serialization option from [Section 4](#4-serialization), may also include semantic validation |
| 0x24 `'$'` | pattern | string | String | Regular expression used to validate a String type ([Section 3.2.1.4](#3214-patterns) |
| 0x7b `'{'` | minv | integer | Integer, Number,<br> Binary, String,<br> Array, ArrayOf,<br> Map, MapOf, Record | Minimum numeric value, octet or character count, or element count |
| 0x7d `'}'` | maxv | integer | Integer, Number,<br> Binary, String,<br> Array, ArrayOf,<br> Map, MapOf, Record | Maximum numeric value, octet or character count, or element count |
| 0x21 `'!'` | default | string | Any | Default value for an instance of this type |

Within a type definition,
* TypeOptions MUST contain zero or one instance of each type option except 0x2f (serialization option).
* For each serialization format, TypeOptions MUST contain zero or one serialization option defined by that format.

#### 3.2.1.1 id

The Enumerated, Choice, and Map types have "named" and "unnamed" variants. Presence of the "id" option in a definition of those types indicates that the type is unnamed. The Record type is always named and has no "id" option; the Array type is its unnamed equivalent.

* In named types, FieldName is a defined name that is included in the semantics of the type, must be populated in the type definition, may appear in serialized data, and cannot be changed.
* In unnamed types, FieldName is a suggested label that is not included in the semantics of the type, may be empty in the type definition, never appears in serialized data, and may be freely customized without affecting interoperability.

For example a list of HTTP status codes could include the field [403, "Forbidden"].  If the Enumerated type definition does not include the "id" option, serialization rules determine whether the id or name is used in protocol data, and the name "Forbidden" cannot be changed. With the "id" option only the id 403 is used in protocol data, but the label "Forbidden" could be displayed in messages or user interfaces, as could customized labels such as "Not Allowed", "Verboten", or "Interdit".

#### 3.2.1.2 vtype and ktype

#### 3.2.1.3 Semantic Validation Keywords
*format*

*sopt - Serialization options may include value constraints applicable to all data formats.*
* IM value is an IPv4 address as defined in [RFC 791](#rfc791).
* IM value is an IPv6 address as defined in [RFC 8200](#rfc8200). 
* IM value is an IPv4 address and a prefix length as specified in Section 3.1 of [RFC 4632](#rfc4632).
* IM value is an IPv6 address and a prefix length as specified in Section 2.3 of [RFC 4291](#rfc4291).

#### 3.2.1.4 Patterns
*pattern*

#### 3.2.1.5 Size and Value Constraints
*minv*, *maxv*

### 3.2.2 Field Options
Field options apply to one field within a type definition.

If FieldType is a JADN type ([Table 3-1](#table-3-1-jadn-types)), FieldOptions may contain type options applicable to that FieldType.
If FieldType is not a JADN type, FieldOptions MUST NOT contain any type options ([Table 3-2](#table-3-2-type-options)).

FieldOptions MUST contain zero or one instance of each of the following field options:  

###### Table 3-3. Field Options

| ID | Label | Type | Definition |
| --- | --- | --- | --- |
| 0x5b `'['` | minc | integer | Minimum cardinality |
| 0x5d `']'` | maxc | integer | Maximum cardinality |
| 0x26 `'&'` | tfield | enum | field that specifies the type of this field |

### 3.2.3 Syntactic Sugar
JADN includes several options that make type definitions more compact or that support the [DRY](#dry) software design principle:
* Type Definition within fields -> Explicit type definition
* Field Multiplicity -> Explicit ArrayOf
* Derived Enumerated -> Explicit Enumerated
* MapOf with Enumerated key -> Explicit Map

These are stylistic options that can be eliminated without affecting the meaning of a type definition. Removing these options simplifies a type definition but creates additional definitions to support it.  This simplifies the code needed to serialize and validate data instances, and may make the original definition easier to understand.

#### Type Definition within fields
#### Field Multiplicity
#### Derived Enumerated
#### MapOf with Enumerated key

# 4 Serialization

Applications may use any internal information representation that exhibits the characteristics defined in [Table 3-1](#table-3-1-jadn-types). Serialization rules define how to represent instances of each type using a specific format. Several serialization formats are defined in this section. Additional serialization formats defined elsewhere are valid if they:
* Specify an unambiguous serialized representation for each JADN type
* Specify how each option applicable to a type affects serialized values
* Specify any value constraints defined for that format

## 4.1 JSON Serialization

The following JSON serialization rules are used to represent JADN data types in a human-friendly format.

When using JSON serialization, instances of JADN types without a serialization option defined in this section MUST be serialized as:

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
* API values MUST satisfy semantic validation requirements associated with a serialization option.

When using JSON serialization, instances of JADN types with one of the following options MUST be serialized as:

| Option | JADN Type | JSON Serialization Requirement | Semantic Validation Requirement |
| :--- | :--- | :--- | :--- |
| **/x** | Binary | JSON **string** containing Base16 (hex) encoding of a binary value as defined in Section 8 of [RFC 4648](#rfc4648). Note that the Base16 alphabet does not include lower-case letters. | None |
| **/ipv4-addr** | Binary | JSON **string** containing a "dotted-quad" as specified in Section 3.2 of [RFC 2673](#rfc2673). | Address as specified in Section 3.1 of [RFC 791](#rfc791) |
| **/ipv6-addr** | Binary | JSON **string** containing the text representation of an IPv6 address as specified in Section 4 of [RFC 5952](#rfc5952). | Address as specified in Section 3 of [RFC 8200](#rfc8200) |
| **/ipv4-net** | Array | JSON **string** containing the text representation of an IPv4 address range as specified in Section 3.1 of [RFC 4632](#rfc4632). | Two components as specified in [RFC 4632](#rfc4632): Binary IPv4 address and Integer prefix length. |
| **/ipv6-net** | Array | JSON **string** containing the text representation of an IPv6 address range as specified in Section 2.3 of [RFC 4291](#rfc4291). | Two components as specified in [RFC 4291](#rfc4291): Binary IPv6 address and Integer prefix length. |

## 4.2 CBOR Serialization

The following serialization rules are used to represent JADN data types in Concise Binary
Object Representation [CBOR] format, where CBOR type #x.y = Major type x, Additional information y.
* The id TypeOption does not affect serialized values.

CBOR type names from Concise Data Definition Language [CDDL] are shown for reference.

When using CBOR serialization, instances of JADN types without a serialization option defined in this section MUST be serialized as:

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
* API values MUST satisfy semantic validation requirements associated with a serialization option.

When using CBOR serialization, instances of JADN types with one of the following options MUST be serialized as:

| Option | JADN Type | CBOR Serialization Requirement | Semantic Validation Requirement |
| :--- | :--- | :--- | :--- |
| **/f16** | Number | **float16**: IEEE 754 Half-Precision Float (#7.25). | None |
| **/f32** | Number | **float32**: IEEE 754 Single-Precision Float (#7.26). | None |

## 4.3 M-JSON Serialization:

Minimized JSON serialization rules represent JADN data types in a compact format optimized for machine-to-machine communication.  They produce JSON instances identical to CBOR serialization using the JSON preface defined in [CDDL] Appendix E. As with CBOR,
* Serialization and id TypeOptions do not affect serialized values.

When using M-JSON serialization, instances of JADN types MUST be serialized as:

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

*Editor's Note: Define XML rules*

When using XML serialization, instances of JADN types MUST be serialized as:

| JADN Type | XML Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Enumerated** | JSON **integer** |
| **Choice** | JSON **object** with one member. Member key is the FieldID converted to string. |
| **Array** | JSON **array** of values with types positionally specified by FieldType. |
| **ArrayOf** | JSON **array**, or JSON **null** if *vtype* is Null. |
| **Map** | JSON **object**. Member keys are FieldIDs converted to strings with value has the . |
| **MapOf** | JSON **object**, or JSON **null** if *vtype* is Null. Members have key type *ktype* and value type *vtype*. |
| **Record** | Same as **Array**. |

# 5 JADN Schema Formats
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

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
## Table format
## JSON format
## CBOR format

# Appendix D. JSON-Schema Data Model for JADN
JSON Schema generated from the IM of Appendix C, validates any JADN schema in JSON format
# Appendix E. CDDL Data Model for JADN
CDDL generated from the IM of Appendix C, validates any JADN schema in CBOR format
