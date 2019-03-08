
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
* JADN Schemas: (JSON, CDDL)

### Related work:

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

(Note: Publication URIs are managed by OASIS TC Administration; please don't modify.)

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

*Capabilities developed in XML, various means to move to JSON, then CBOR.*

*Standards are created using data definition tables with a goal of being agnostic of transfer format, but no well-defined mechanism exists for achieving that goal. JADN defines a table structure that translates completely and unambiguously to a machine-usable schema. The schema serves as "byte code" that can be transferred between applications and interpreted to validate application data. It can be embedded to produce self-describing data.*

*Numerous data definition languages are in use. JADN doesn't replace any of them, but serves as a Rosetta stone to facilitate translation among them.*

The text in this section may all be replaced, but the following three sections (1.1, 1.2, and 1.3) are required for OASIS publications. Section 1.1 (IPR Policy) must not be changed by the TC. Section 1.2 (Terminology) may be modified to include other terminology-related information used in this specification. Section 1.3 (Normative References) should be modified to include additional references, as needed. Section 1.4 (Non-Normative References) is not required, but should be modified to include additional references, as needed.

Here is a customized command line which will generate HTML from this markdown file (named jadn-v1.0-wd01.md):

pandoc -f gfm -t html jadn-v1.0-wd01.md -c styles/markdown-styles-v1.7.css --toc --toc-depth=5 -s -o jadn-v1.0-wd01.html --metadata title="Specification for JSON Abstract Data Notation Version 1.0"

We are currently using pandoc 2.6 from https://github.com/jgm/pandoc/releases/tag/2.6.

This also requires the presence of a .css file containing the HTML styles (like styles/markdown-styles-v1.7.css).

Note this command generates a Table of Contents (TOC) in HTML which is located at the top of the HTML document, and which requires additional editing in order to be published in the expected OASIS style. This editing will be handled by OASIS staff during publication.

## 1.1 IPR Policy
This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode) Mode of the [OASIS IPR Policy](https://www.oasis-open.org/policies-guidelines/ipr), the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page ([https://www.oasis-open.org/committees/openc2/ipr.php](https://www.oasis-open.org/committees/openc2/ipr.php)).

## 1.2 Terminology
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [[RFC2119](#rfc2119)] and [[RFC8174](#rfc8174)] when, and only when, they appear in all capitals, as shown here.

## 1.3 Normative References

(Reference sources:
For references to IETF RFCs, use the approved citation formats at:  
http://docs.oasis-open.org/templates/ietf-rfc-list/ietf-rfc-list.html.  
For references to W3C Recommendations, use the approved citation formats at:  
http://docs.oasis-open.org/templates/w3c-recommendations-list/w3c-recommendations-list.html.  
Remove this note before submitting for publication.)

###### [RFC2119]
Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997, http://www.rfc-editor.org/info/rfc2119.
###### [RFC8174]
Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174, May 2017, http://www.rfc-editor.org/info/rfc8174.

## 1.4 Non-Normative References

###### [MDA]
*"The Fast Guide to Model Driven Architecture"*, https://www.omg.org/mda/mda_files/Cephas_MDA_Fast_Guide.pdf

###### [RFC791]


###### [RFC2673]
*"Binary Labels in the Domain Name System"*, https://tools.ietf.org/html/rfc2673

###### [RFC3444]
*"On the Difference between Information Models and Data Models"*, https://tools.ietf.org/html/rfc3444

###### [RFC3552]
Rescorla, E. and B. Korver, "Guidelines for Writing RFC Text on Security Considerations", BCP 72, RFC 3552, DOI 10.17487/RFC3552, July 2003, https://www.rfc-editor.org/info/rfc3552.

## 1.5 Some markdown usage examples

**Text.**

Note that text paragraphs in markdown should be separated by a blank line between them -

Otherwise the separate paragraphs will be joined together when the HTML is generated.
Even if the text appears to be separate lines in the markdown source.

To avoid having the usual vertical space between paragraphs,  
append two or more space characters to the end of the lines  
which will generate an HTML break tag instead of a new paragraph tag  
(as demonstrated here).

### 1.5.1 Figures and Captions

FIGURE EXAMPLE:
<note caption is best ABOVE figure, to allow a link to it to display image - same for table captions>

###### Figure 1 -- Title of Figure
![image-label should be meaningful](images/image_0.png) (this image is missing)

###### Figure 2 -- OpenC2 Message Exchange
![message exchange](images/image_1.png)


### 1.5.2 Tables

#### 1.5.2.1 Basic Table
**Table 1-1. Table Label**

| Item | Description |
| :--- | :--- |
| Item 1 | Something<br>(second line) |
| Item 2 | Something |
| Item 3 | Something<br>(second line) |
| Item 4 | text |

#### 1.5.2.2 Table with Three Columns and Some Bold Text
text.

| Title 1 | Title 2 | title 3 |
| :--- | :--- | :--- |
| something | something | something else that is a long string of text that **might** need to wrap around inside the table box and will just continue until the column divider is reached |
| something | something | something |

#### 1.5.2.3 Table with a caption which can be referenced

###### Table 1-5. See reference label construction

| Name | Description |
| :--- | :--- |
| **content** | Message body as specified by content_type and msg_type. |

Here is a reference to the table caption:
Please see [Table 1-5 or other meaningful label](#table-1-5-see-reference-label-construction) 


### 1.5.3 Lists

Bulleted list:
* bullet item 1.
* **Bold** bullet item 2.
* bullet item 3.
* bullet item 4.

Indented or multi-level bullet list - add two spaces per level before bullet character (* or -):
* main bullet type
  * Example second bullet
    * See third level
      * fourth level

Numbered list:
1. item 1
2. item 2
3. item 3

### 1.5.4 Reference Label Construction

REFERENCES and ANCHORS
- in markdown source, format the Reference tags as level 6 headings like: `###### [RFC2119]`
###### [RFC2119]
Bradner, S., "Key words ..."

- reference text has to be on a separate line below the tag

- format cross-references (citations of the references) like: `see [[RFC2119](#rfc2119)]`  
"see [[RFC2119](#rfc2119)]"  
(note the outer square brackets in markdown will appear in the visible HTML text)

- The text in the Reference tag (following ###### ) will become an HTML anchor using the following conversion rules:  
-- punctuation marks will be dropped (including "[" )  
-- leading white spaces will be dropped  
-- upper case will be converted to lower  
-- spaces between letters will be converted to a single hyphen

- The same HTML anchor construction rules apply to cross-references and to section headings.  
-- Thus, a section heading like "## 1.3 Normative References"  
-- becomes an anchor in HTML like `<a href="#13-normative-references">`  
-- referenced in the markdown like: see [Section 1.3](#13-normative-references)  
-- (in markdown: `"see [Section 1.3](#13-normative-references"`)  
-- similar HTML anchors are also used in constructing the TOC

### 1.5.5 Code Blocks

Text to appear as an indented code block with grey background and monospace font - use three back-ticks before and after the code block).

Note the actual backticks will not appear in the HTML version. If it's necessary to display visible backticks, place a back-slash before them like: \``` .

```
{   
    "target": {
        "x_kmip_2.0": {
            {"kmip_type": "json"},
            {"operation": "RekeyKeyPair"},
            {"name": "publicWebKey11DEC2017"}
        }
    }
}
```

Text to be highlighted as code can also be surrounded by a single "backtick" character: 
`code text`

## 1.6 Page Breaks
Add horizontal rule lines where page breaks are desired in the PDF - before each major section
- insert the line rules in markdown by inserting 3 or more hyphens on a line by themselves:  ---
- place these before each main section in markdown (usually "#" - which generates the HTML `<h1>` tag)

-------

# 2 Information vs. Data
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
contained in a message.  When information is coded for transmission in a canonical format, the additional
data used for purposes such as text conversion, delimiting, and framing contains no entropy because it is known a priori.
If the serialization is non-canonical, any additional entropy introduced during serialization
(e.g., whitespace, leading zeroes, case-insensitive capitalization) is discarded on deserialization.

For example, an IPv4 address [RFC791] contains 32 bits of information. But different data may be used to
represent the same information:
* IPv4 dotted-quad [RFC2673] contained in a JSON string: "192.168.141.240" (17 bytes / 136 bits).
* Hex value contained in a JSON string: "C0A88DF0" (10 bytes / 80 bits)
* CBOR byte string: 0x44c0a88df0 (5 bytes / 40 bits).

JADN is based on the CBOR data model (JSON types plus integers, special numbers, and byte strings), but has an
information-centric focus:

| Data-centric | Information-centric |
| --- | --- |
| JSON Schema defines integer as a value constraint on the JSON number type: "integer matches any number with a zero fractional part". | Integer and Number first-class types exist regardless of data representation. |
| CDDL says: "While CBOR map and array are only two representation formats, they are used to specify four loosely-distinguishable styles of composition". | Five first-class types represent distinct composition styles. |
| No table composition style is specified. | Tables are a fundamental way of organizing information. The Record first class type can represent tabular information in both array and map formats. |
| Data-centric design is often Anglocentric. | Information-centric types encourage definition of natural-language-agnostic protocols. |

# 3 JADN Types
JADN first-class types are defined in terms of their characteristics:

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
| Enumerated | One value selected from a set of named integers. |
| Enumerated.ID | One value selected from a set of unnamed integers. |
| Choice | One field selected from a set of named fields. The value has an id, name, and type. |
| Choice.ID | One field selected from a set of unnamed fields.  The value has an id and type. |
| Array | An ordered list of unnamed fields that have positionally-defined types. Each field has a position and a type. Corresponds to CDDL *record*. |
| ArrayOf(*vtype*) | An ordered list of unnamed fields that have the same type. Each field has a position and type *vtype*. Corresponds to CDDL *vector*. |
| Map | An unordered set of named fields. Each field has an id, name, and type. Corresponds to CDDL *struct*. |
| Map.ID | An unordered set of unnamed fields.  Each field has an id and type. |
| MapOf(*ktype*, *vtype*) | An unordered set of fields that have the same type. Each field has key type *ktype* and value type *vtype*. Represents a map with keys that are either enumerated or are members of a well-defined category. Corresponds to CDDL *table*. |
| Record | An ordered set of named fields. Each field has a position, name, and type. Represents a row in a spreadsheet or database table. CDDL has no corresponding composition style. |

Each field in a structured type definition has both an integer id and a string name. The Enumerated, Choice, and Map first-class types have ".ID" variants where fields are "unnamed".  The difference is that with the named variants, names are included in the semantics of the type, must be populated in the type definition, and may appear in serialized data. With the unnamed variants, names are not included in the semantics, may be empty in the type definition, never appear in serialized data, but if present they may be used as non-normative labels. Field names within ".ID" type definitions may be freely customized without affecting interoperability.

For example a list of HTTP status codes could include the field (403, "Forbidden").  With the Enumerated type, serialization rules determine whether the id or name is used in protocol data. With the Enumerated.ID type only the id 403 is used in protocols, but the label "Forbidden" could be displayed in messages or user interfaces, as could customized labels such as "Not Allowed", "Verboten", or "Interdit".

## 3.1 Type Definitions
JADN type definitions have a simple, regular structure designed to be both easily processed and extensible. Each JADN type definition has four elements, plus for some types, a list of fields:

1. **TypeName:** the name of the type being defined
2. **BaseType:** the JADN type of the type being defined
3. **TypeOptions:** a list of zero or more options applicable to the type being defined
4. **TypeDescription:** a non-normative comment
5. **Fields:** a list of one or more field definitions, if applicable to BaseType

Primitive, ArrayOf, and MapOf base types have no field definitions.

Field definitions for the Enumerated base type have three elements:
1. **FieldID:** the integer identifier of the field
2. **FieldName:** the name of the field
3. **FieldDescription:** a non-normative comment

Field definitions for the Array, Choice, Map, and Record base types have five elements:
1. **FieldID:** the integer identifier of the field
2. **FieldName:** the name of the field
3. **FieldType:** the type of the field
4. **FieldOptions:** a list of zero or more options applicable to the field
5. **FieldDescription:** a non-normative comment

FieldID and FieldName values MUST be unique within a type definition.
For Array and Record base types, FieldID MUST be the position of the field within the type, numbered consecutively starting at 1.
For Enumerated, Choice and Map base types, FieldID may be any integer tag that does not conflict with another field within the type.

## 3.2 Options

### 3.2.1 Type Options
| Option ID | Type | Definition |
| --- | --- | --- |
| 0x3d `=` | boolean | id: If present, type is an ".ID" variant where FieldName is a non-normative label |
| 0x2f `/` | string | sopt: Semantic validation keyword and serialization option |
| 0x40 `@` | string | fmt: Semantic validation keyword |
| 0x7b `{` | integer | minv: Minimum string length, integer value, array length, property count |
| 0x7d `}` | integer | maxv: Maximum string length, integer value, array length, property count |
| 0x2a `*` | string | vtype: ArrayOf/MapOf element type, or Enumerated value from the named type  |
| 0x2b `+` | string | ktype: MapOf key type |
| 0x24 `$` | string | pat: regular expression used to validate a String type |
| 0x21 `!` | string | def: default value for an instance of this type |

Within a type definition,
* TypeOptions MUST contain no more than one instance of any option except 0x2f (serialization option).
* TypeOptions MUST contain no more than one serialization option defined for any serialization format.

### 3.2.2 Field Options
FieldOptions may include 
| Option ID | Type | Definition |
| --- | --- | --- |
| 0x5b `[` | integer | minc: Minimum cardinality |
| 0x5d `]` | integer | maxc: Maximum cardinality |
| 0x26 `&` | enum | tfield: field that specifies the type of this field |

### 3.2.3 Semantic Validation Keywords
Non-transforming (email)
Serialization options include value constraints
* IM value is an IPv4 address as defined in [RFC791].
* IM value is an IPv6 address as defined in [RFC8200]. 
* IM value is an IPv4 address and a prefix length as specified in Section 3.1 of RFC 4632.
* IM value is an IPv6 address and a prefix length as specified in Section 2.3 of RFC 4291.

# 4 Serialization
Serialization rules define how to represent an instance of a type using a specific data format.  Several serialization formats are defined here.  Other documents may define additional serialization formats by specifying an unambiguous representation of each JADN type.

## 4.1 JSON Serialization

The following JSON serialization rules are used to represent JADN data types in a human-friendly format.

When using JSON serialization, instances of JADN types without a serialization option defined in this section MUST be serialized as:

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
| **Choice** | JSON **object** with one member.  Member key is FieldName.   |
| **Choice.ID** | JSON **object** with one member. Member key is FieldID converted to string. |
| **Enumerated** | JSON **string** |
| **Enumerated.ID** | JSON **integer** |
| **Map** | JSON **object**. Member keys are FieldNames. |
| **Map.ID** | JSON **object**. Member keys are FieldIDs converted to strings. |
| **MapOf** | JSON **object**. Member keys are instances of *ktype*. |
| **Record** | JSON **object**. Member keys are FieldNames. |

**JSON Serialization Options**
* JADN type definitions with more than one of the following options are invalid.
* JADN type definitions with a type other than that applicable to the option are invalid.

When using JSON serialization, instances of JADN types with one of the following options MUST be serialized as:

| Serialization Option | JADN Type | JSON Serialization Requirement |
| :--- | :--- | :--- |
| **/x** | Binary | JSON **string** containing Base16 (hex) encoding of a binary value as defined in Section 8 of RFC 4648. Note that the Base16 alphabet does not include lower-case letters. |
| **/ipv4-addr** | Binary | JSON **string** containing a "dotted-quad" as specified in Section 3.2 of [RFC2673]. |
| **/ipv6-addr** | Binary | JSON **string** containing the text representation of an IPv6 address as specified in Section 4 of RFC 5952. |
| **/ipv4-net** | Array | JSON **string** containing the text representation of an IPv4 address range as specified in Section 3.1 of RFC 4632. |
| **/ipv6-net** | Array | JSON **string** containing the text representation of an IPv6 address range as specified in Section 2.3 of RFC 4291. | 

## 4.2 CBOR Serialization

The following serialization rules are used to represent JADN data types in Concise Binary
Object Representation [CBOR] format, where CBOR type #x.y = Major type x, Additional information y.
* Serialization options and .ID variants do not affect serialized values.

CBOR type names from Concise Data Definition Language [CDDL] are shown for reference.

When using CBOR serialization, instances of JADN types MUST be serialized as:

| JADN Type | CBOR Serialization Requirement |
| :--- | :--- |
| **Binary** | **bstr**: a byte string (#2). |
| **Boolean** | **bool**: a Boolean value (False = #7.20, True = #7.21). |
| **Integer** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Number** |  **float64**: IEEE 754 Double-Precision Float (#7.27). |
| **Null** | **null**: (#7.22) |
| **String** | **tstr**: a text string (#3). |
| **Array** | **array**: an array of data items (#4) with types specified by FieldType. |
| **ArrayOf** | **vector**: an array of data items (#4) of type *vtype*. |
| **Choice** | **struct**: a map (#5) containing one pair. The first item is a FieldID, the second item has the corresponding FieldType. |
| **Enumerated** | **int**: an unsigned integer (#0) or negative integer (#1) FieldID. |
| **Map** | **struct**: a map (#5) of pairs. In each pair the first item is a FieldID, the second item has the corresponding FieldType. |
| **MapOf** | **table**: a map (#5) of pairs. In each pair the first item has type *ktype*, the second item has type *vtype*. |
| **Record** | **record**: an array of values (#4) with types positionally specified by FieldType. |

## 4.3 M-JSON Serialization:

Minimized JSON serialization rules represent JADN data types in a compact format optimized for machine-to-machine communication.  They produce JSON instances identical to CBOR serialization using the JSON preface defined in [CDDL] Appendix E. As with CBOR,
* Serialization options and .ID variants do not affect serialized values.

When using M-JSON serialization, instances of JADN types MUST be serialized as:

| JADN Type | M-JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Array** | JSON **array** of values with types positionally specified by FieldType. |
| **ArrayOf** | JSON **array** |
| **Choice** | JSON **object** with one member. Member key is the FieldID converted to string. |
| **Enumerated** | JSON **integer** |
| **Map** | JSON **object**. Member keys are FieldIDs converted to strings with value has the . |
| **MapOf** | JSON **object**. Members have key type *ktype* and value type *vtype*. |
| **Record** | JSON **array** of values with types positionally specified by FieldType. |

## 4.4 XML Serialization:

When using XML serialization, instances of JADN types MUST be serialized as:

| JADN Type | XML Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Array** | JSON **array** of values with types positionally specified by FieldType. |
| **ArrayOf** | JSON **array** |
| **Choice** | JSON **object** with one member. Member key is the FieldID converted to string. |
| **Enumerated** | JSON **integer** |
| **Map** | JSON **object**. Member keys are FieldIDs converted to strings with value has the . |
| **MapOf** | JSON **object**. Members have key type *ktype* and value type *vtype*. |
| **Record** | JSON **array** of values with types positionally specified by FieldType. |

# 5 JADN Schema Formats
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

# 6 Data Model Generation
A JADN schema can be combined with a set of serialization rules to produce a DM, a schema applicable to the serialized data format.

-------

# 7 Security Considerations
(Note: OASIS strongly recommends that Technical Committees consider issues that could affect security when implementing their specification and document them for implementers and adopters. For some purposes, you may find it required, e.g. if you apply for IANA registration.

While it may not be immediately obvious how your specification might make systems vulnerable to attack, most specifications, because they involve communications between systems, message formats, or system settings, open potential channels for exploit. For example, IETF [[RFC3552](#rfc3552)] lists “eavesdropping, replay, message insertion, deletion, modification, and man-in-the-middle” as well as potential denial of service attacks as threats that must be considered and, if appropriate, addressed in IETF RFCs. 

In addition to considering and describing foreseeable risks, this section should include guidance on how implementers and adopters can protect against these risks.

We encourage editors and TC members concerned with this subject to read _Guidelines for Writing RFC Text on Security Considerations_, IETF [[RFC3552](#rfc3552)], for more information.

Remove this note before submitting for publication.)

-------

# 8 Conformance
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
| Jason | | |
| Bret | | |
| Brian | | |

-------

# Appendix B. Revision History
| Revision | Date | Editor | Changes Made |
| :--- | :--- | :--- | :--- |
| jadn-v1.0-wd01 | 2019-03-01 | David Kemp | Initial working draft |

# Appendix C. JADN Information Model for JADN
## Table format
## JSON format
## CBOR format

# Appendix D. JSON-Schema Data Model for JADN
JSON Schema generated from the IM of Appendix C, validates any JADN schema in JSON format
# Appendix E. CDDL Data Model for JADN
CDDL generated from the IM of Appendix C, validates any JADN schema in CBOR format
