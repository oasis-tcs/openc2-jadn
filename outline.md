## Abstract
JSON Abstract Data Notation (JADN) is an information modeling language based on the CBOR data model. It has several purposes, including definition of data structures, validation of data instances, providing hints for user interfaces working with structured data, and facilitating protocol internationalization. JADN specifications consist of two parts: abstract type definitions that are independent of data format, and serialization rules that define how to represent type instances using specific data formats.  A JADN schema is itself a structured information object that can be serialized and transferred between applications, documented in multiple formats such as property tables and text-based data definition languages, and translated into concrete schemas used to validate specific data formats.

## Normative References

## Non-Normative References

###### [MDA]
*"The Fast Guide to Model Driven Architecture"*, https://www.omg.org/mda/mda_files/Cephas_MDA_Fast_Guide.pdf

###### [RFC2673]
*"Binary Labels in the Domain Name System"*, https://tools.ietf.org/html/rfc2673

###### [RFC3444]
*"On the Difference between Information Models and Data Models"*, https://tools.ietf.org/html/rfc3444


## 1. Information vs. Data
JSON Abstract Data Notation (JADN) is an information modeling language. 
[RFC3444] describes the difference between an information model (IM) and a data model (DM):
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

In the context of data definitions within a Model Driven Architecture [MDA]:
* An IM is part of a Platform Independent Model (PIM) that exhibits a sufficient degree of independence so as to enable its
mapping to one or more platforms.
* A DM is part of a Platform Specific Model (PSM) that combines the specifications in the PIM with the details
required to stipulate how a system uses a particular type of platform. 

Information is *what* needs to be communicated between applications, and data is *how* that information
is represented when communicating.  More formally, information is the unexpected data, or "entropy",
contained in a message.  When information is serialized for transmission in a canonical format, the additional
data used for purposes such as text conversion, delimiting, and framing contains no entropy because it is known a priori.
If the serialization is non-canonical, any additional entropy introduced during serialization
(e.g., whitespace, case-insensitive capitalization) is discarded on deserialization.

For example, an IPv4 address [RFC791] contains 32 bits of information. But different data may be used to
represent the same information:
* "Dotted-quad" [RFC2673] contained in a JSON string: "192.168.141.240" (17 bytes / 136 bits).
* Hex value contained in a JSON string: "C0A88DF0" (10 bytes / 80 bits)
* CBOR byte string: 0x44c0a88df0 (5 bytes / 40 bits).

JADN is based on the CBOR data model (JSON types plus integers, special numbers, and byte strings), but it has an
information-centric focus:

| Data-centric | Information-centric |
| --- | --- |
| JSON Schema defines integer as a value constraint on the JSON number type: "integer matches any number with a zero fractional part". | Distinct first-class types for Integer and Number. |
| CDDL says: "While CBOR map and array are only two representation formats, they are used to specify four loosely-distinguishable styles of composition". | Five first-class types represent distinct composition styles. |
| No table-specific schema support. | Tables are a fundamental way of organizing information. The Record first-class type enables both map and array representations of tabular data. |
| Data-centric protocols are often designed to be Anglocentric | Information-centric types support definition of natural-language-agnostic protocols. |

## 2. JADN Types
The JADN built-in (base) types are defined in terms of their characteristics:

| JADN Type | Definition |
| :--- | :--- |
| **Primitives** |   |
| Binary | A sequence of octets.  Length is the number of octets. |
| Boolean | An element with one of two values: true or false. |
| Integer | A whole number. |
| Number | A real number. |
| Null | An unspecified or non-existent value. |
| String | A sequence of characters, each of which has a Unicode codepoint.  Length is the number of characters. |
| **Structures** |   |
| Enumerated | One value selected from a set of named integers. |
| Enumerated.ID | One value selected from a set of unnamed integers. |
| Choice | One field selected from a set of named fields. The value has an id, name, and type. |
| Choice.ID | One field selected from a set of unnamed fields.  The value has an id and type. |
| Array | An ordered list of unnamed fields that have positionally-defined types. Each field has a position and a type. Corresponds to CDDL *record*. |
| ArrayOf(*vtype*) | An ordered list of unnamed fields that have the same type. Each field has a position and type *vtype*. Corresponds to CDDL *vector*. |
| Map | An unordered set of named fields. Each field has an id, name, and type. Corresponds to CDDL *struct*. |
| Map.ID | An unordered set of unnamed fields.  Each field has an id and type. |
| MapOf(*ktype*, *vtype*) | An unordered set of fields that have the same type. Each field has key type *ktype* and value type *vtype*. Represents a map with keys that are either enumerated or members of a well-defined category. Corresponds to CDDL *table*. |
| Record | An ordered set of named fields. Each field has a position, name, and type. Represents a row in a spreadsheet or database table. CDDL has no corresponding composition style. |

Every field in structured types has both an integer id and a string name. The Enumerated, Choice, and Map types have ".ID" variants where fields are "unnamed".  The difference is that with the named variants, the name is included in the semantics of the type, must be populated in the type definition, and may appear in serialized data. With the unnamed variants names are not included in the semantics, may be empty in the type definition, never appear in serialized data, but if populated they may be used as non-normative labels. Field names within ".ID" type definitions may be freely customized without affecting interoperability.

For example a list of HTTP status codes could include the field (403, "Forbidden").  With the Enumerated type, serialization rules determine whether the id or the name is used in protocol data.  With the Enumerated.ID type only the id 403 is used in protocols, but the label "Forbidden" could appear in messages or user interfaces, as could customized labels such as "Not Allowed", "Verboten", or "Interdit".

### 2.1. Type Definitions
The JADN type definition format is designed to be 1) easily processed, with a fixed, regular structure, and 2) easily extended, without affecting the structure, through use of options. Each type definition consists of four elements, plus for compound types, a list of fields:

1. **TypeName:** the name of the type being defined
2. **BaseType:** the name of the built-in type that the type being defined is based on
3. **TypeOptions:** a list of zero or more options applicable to the type being defined
4. **TypeDescription:** a non-normative comment
5. **Fields:** if applicable to BaseType, a list of one or more field definitions

A JADN field defintion consists of:
1. **ID:** the integer identifier of the field
2. **FieldName:** the name of the field

### 2.2. Options

#### 2.2.1. Structural Options

#### 2.2.2. Value Constraints

pure constraints
serialization option constraints

#### 2.2.3. Semantic Validation Keywords
Non-transforming (email)
Serialization options include value constraints
* IM value is an IPv4 address as defined in [RFC791].
* IM value is an IPv6 address as defined in [RFC8200]. 
* IM value is an IPv4 address and a prefix length as specified in Section 3.1 of RFC 4632.
* IM value is an IPv6 address and a prefix length as specified in Section 2.3 of RFC 4291.

## 3. Serialization
Serialization rules define how to represent an instance of a type using a specific data format.  Three serialization formats are defined here.  Other documents may define additional serialization formats by specifying an unambiguous representation of each JADN type.

### 3.1 JSON Serialization

The following JSON serialization rules are used to represent JADN data types in a human-friendly format, where:
1) Records are serialized as objects
2) Enumerated values and Object keys are serialized as meaningful strings, or as integer IDs if the .ID suffix is specified
3) Binary values are serialized using type-specific text representations if a serialization option (e.g., /x) is specified

When using JSON serialization:
* 3.1.1. Instances of JADN types without a serialization option defined in this section MUST be serialized as:

| JADN Type | JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Array** | JSON **array** |
| **ArrayOf** | JSON **array** |
| **Choice** | JSON **object** with one member.  Member key is the field name.   |
| **Choice.ID** | JSON **object** with one member. Member key is the integer id converted to string. |
| **Enumerated** | JSON **string** |
| **Enumerated.ID** | JSON **integer** |
| **Map** | JSON **object**. Member keys are field names. |
| **Map.ID** | JSON **object**. Member keys are integer ids converted to strings. |
| **MapOf** | JSON **object**. Member keys are specified by enum type. |
| **Record** | JSON **object**. Member keys are field names. |

**JSON Serialization Options**
JADN type definitions with more than one of the following options are invalid.
JADN type definitions with a type other than that applicable to the option are invalid.
* 3.1.2. Instances of JADN types with one of the following options MUST be serialized as:

| Serialization Option | JADN Type | JSON Serialization Requirement |
| :--- | :--- | :--- |
| **/x** | Binary | JSON **string** containing Base16 (hex) encoding of a binary value as defined in Section 8 of RFC 4648. Note that the Base16 alphabet does not include lower-case letters. |
| **/ipv4-addr** | Binary | JSON **string** containing the text representation of an IPv4 address as specified in Section 3 of "Textual Representation of IPv4 and IPv6 Addresses" [TEXTREP]. |
| **/ipv6-addr** | Binary | JSON **string** containing the text representation of an IPv6 address as specified in Section 4 of RFC 5952. |
| **/ipv4-net** | Array | JSON **string** containing the text representation of an IPv4 address range as specified in Section 3.1 of RFC 4632. |
| **/ipv6-net** | Array | JSON **string** containing the text representation of an IPv6 address range as specified in Section 2.3 of RFC 4291. | 

### 3.2 CBOR Serialization

The following serialization rules are used to represent JADN data types in Concise Binary
Object Representation [CBOR] format, where CBOR type #x.y = Major type x, Additional information y.
* Serialization options (e.g., /x) do not affect serialized values.
* The .ID suffix on Choice, Enumerated and Map types does not affect serialized values.

CBOR type names from Concise Data Definition Language [CDDL] are shown here for reference.

When using CBOR serialization:
* 3.2.1. Instances of JADN types MUST be serialized as:

| JADN Type | CBOR Serialization Requirement |
| :--- | :--- |
| **Binary** | **bstr**: a byte string (#2). |
| **Boolean** | **bool**: a Boolean value (False = #7.20, True = #7.21). |
| **Integer** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Number** |  **float64**: IEEE 754 Double-Precision Float (#7.27). |
| **Null** | **null**: (#7.22) |
| **String** | **tstr**: a text string (#3). |
| **Array** | **array**: an array of data items (#4). |
| **ArrayOf** | **vector**: an array of data items (#4). |
| **Choice** | **struct**: a map (#5) containing one pair. The first item (key) is an integer id, the second item is the value. |
| **Choice.ID** | **struct**: a map (#5) containing one pair. The first item (key) is an integer id, the second item is the value. |
| **Enumerated** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Enumerated.ID** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Map** | **struct**: a map (#5) of pairs. In each pair the first item (key) is an integer id, the second item is the value. |
| **Map.ID** | **struct**: a map (#5) of pairs. In each pair the first item (key) is an integer id, the second item is the value. |
| **MapOf** | **table**: a map (#5) of pairs. In each pair the first item (key) is an integer id, the second item is the value. |
| **Record** | **record**: an array of data items (#4). |

### 3.3 M-JSON Serialization:

Minimized JSON serialization rules represent JADN data types in a compact format optimized for machine-to-machine communication.  They produce JSON instances identical to CBOR serialization using the JSON preface defined in [CDDL] Appendix E.
1) Records are serialized as arrays
2) Enumerated values are serialized as integers
3) Object keys are serialized as integer ids in string format
4) Binary values are serialized as Base64url strings

As with CBOR,
* Serialization options (e.g., /x) do not affect serialized values.
* The .ID suffix on Choice, Enumerated and Map types does not affect serialized values.

When using M-JSON serialization:
* 3.3.1. Instances of JADN types MUST be serialized as:

| JADN Type | M-JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Array** | JSON **array** |
| **ArrayOf** | JSON **array** |
| **Choice** | JSON **object** with one member. Member key is the integer id converted to string. |
| **Choice.ID** | JSON **object** with one member. Member key is the integer id converted to string. |
| **Enumerated** | JSON **integer** |
| **Enumerated.ID** | JSON **integer** |
| **Map** | JSON **object**. Member keys are integer ids converted to strings. |
| **Map.ID** | JSON **object**. Member keys are integer ids converted to strings. |
| **MapOf** | JSON **object**. Member keys are integer ids converted to strings. |
| **Record** | JSON **array**. |

## 4. JADN Schema Formats
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

## 5. Data Model Generation
A JADN schema can be combined with a set of serialization rules to produce a DM, a schema applicable to the serialized data format.
