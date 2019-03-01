## Abstract
JSON Abstract Data Notation (JADN) is an information modeling language. It is based on the CBOR data model (JSON types plus integers, special numbers, and byte strings), but JADN types are information-centric rather than data-centric. JADN-based specifications consist of two parts: abstract type definitions that are independent of data format, and serialization rules that define how to represent an instance of a type using a specific data format.  A JADN schema is a structured information object that can be serialized and transferred between applications, displayed in multiple documentation formats such as tables and text-based data definition languages, and translated into concrete schemas for specific data formats.

## Non-Normative References

###### [TEXTREP]
*"Textual Representation of IPv4 and IPv6 Addresses"*, https://tools.ietf.org/html/draft-main-ipaddr-text-rep-02#section-3.1

###### [MDA]
*"The Fast Guide to Model Driven Architecture"*, https://www.omg.org/mda/mda_files/Cephas_MDA_Fast_Guide.pdf

###### [RFC3444]
*"On the Difference between Information Models and Data Models"*, https://tools.ietf.org/html/rfc3444

## 1. Information vs. Data
This section is Non-Normative.

JSON Abstract Data Notation (JADN) is an information modeling language. 
RFC 3444 describes the difference between an information model (IM) and adata model (DM):
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
* A DM is part of a Platform Specific model (PSM) that combines the specifications in the PIM with the details
required to stipulate how a system uses a particular type of platform. 

Information is *what* needs to be communicated between applications, and data is *how* that information
is represented when communicating.  More formally, information theory defines information as the unexpected data or
"entropy" contained in a message.  When information is serialized for transmission in a canonical format, the additional
data used for purposes such as text conversion, delimiting and framing contains no entropy because it is known a priori.
If the serialization is non-canonical, any additional entropy introduced into the data during serialization
(e.g., whitespace) is discarded on deserialization.

For example, in an IM an IPv4 address [RFC791] is a 32 bit value because it contains 32 bits of
information that applications care about.  Different DMs define how an IPv4 address is serialized, for example:
* IPv4 Dotted Octet Format [TEXTREP] contained in a JSON string: "192.168.141.240" (17 bytes / 136 bits of data).
* Hex value contained in a JSON string: "C0A88DF0" (10 bytes / 80 bits)
* CBOR byte string: 0x44c0a88df0 (5 bytes / 40 bits).

The serialized data is different when using different DMs, but these instances all represent the same 32 bit information value.

## 2. JADN Types

JADN type definitions provide:
* Value constraints (enumerations, size and value ranges, regex patterns, semantic validation keywords)
* Names for enumerated values and structure fields
* Structure composition styles similar to CDDL
* Serialization options

For structure types, arrays and maps are
the only two representation formats, but they are used to specify five distinguishable styles of composition:
* **vector**, an array of elements that have the same semantics.
* **array**, an array of elements that have different positionally-defined semantics, as detailed in the structure definition.
* **table**, a map from a domain of keys to a domain of values that have the same semantics.
* **struct**, a map from a domain of keys as defined by the specification to a domain of values that have semantics bound to the key.
* **record**, an ordered map from keys that have positions to values that have positionally-defined semantics, as detailed in the structure definition.

## 3. Serialization
Serialization rules define how to represent an instance of a type using a specific data format.  Three serialization formats are defined here.  Other documents may define additional serialization formats by specifying an unambiguous representation of each JADN type.

### 3.1 JSON Serialization

The following JSON serialization rules are used to represent JADN data types in a human-friendly format, where:
1) Records are serialized as objects
2) Enumerated values and Object keys are serialized as meaningful strings, or as integer IDs if the .ID suffix is specified
3) Binary values are serialized using type-specific text representations if if specified with a serialization option (e.g., /x)

When using JSON serialization:
* 3.1.1. Instances of JADN types without serialization options MUST be serialized as:

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
* 3.1.2. Serialization options other than those defined below MUST be ignored
* 3.1.3. Instances of JADN types with the following serialization options MUST be serialized as:

| Serialization Option | Type | JSON Serialization Requirement |
| :--- | :--- | :--- |
| **/x** | Binary | JSON **string** containing Base16 (hex) encoding of a binary value as defined in Section 8 of RFC 4648. Note that the Base16 alphabet does not include lower-case letters. |
| **/ipv4-addr** | Binary | JSON **string** containing the text representation of an IPv4 address as specified in Section 3 of "Textual Representation of IPv4 and IPv6 Addresses" [TEXTREP].  IM value is a binary IPv4 address as defined in [RFC791]. |
| **/ipv6-addr** | Binary | JSON **string** containing the text representation of an IPv6 address as specified in Section 4 of RFC 5952. IM value is a binary IPv6 address as defined in [RFC8200]. |
| **/ipv4-net** | Array | JSON **string** containing the text representation of an IPv4 address range as specified in Section 3.1 of RFC 4632. IM value is a two element array containing a binary IPv4 address and an integer prefix length. |
| **/ipv6-net** | Array | JSON **string** containing the text representation of an IPv6 address range as specified in Section 2.3 of RFC 4291. IM value is a two element array containing a binary IPv6 address and an integer prefix length. | 

### 3.2 CBOR Serialization

The following serialization rules are used to represent JADN data types in Concise Binary
Object Representation [CBOR] format, where CBOR type #x.y = Major type x, Additional information y.
* Serialization options (e.g., /x) do not affect serialized values.
* The .ID suffix on Choice, Enumerated and Map types does not affect serialized values.

CBOR type names from Concise Data Definition Language [CDDL] are shown here for reference.

When using CBOR serialization:
* 3.2.1. Serialization options MUST be ignored
* 3.2.2. Instances of JADN types MUST be serialized as:

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
| **Choice, Choice.ID** | **struct**: a map (#5) containing one pair. The first item (key) is an integer id, the second item is the value. |
| **Enumerated, Enumerated.ID** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Map, Map.ID**| **struct**: a map (#5) of pairs. In each pair the first item (key) is an integer id, the second item is the value. |
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

When using CBOR serialization:
* 3.2.1. Serialization options MUST be ignored
* 3.2.2. Instances of JADN types MUST be serialized as:

| JADN Type | M2M JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Array** | JSON **array** |
| **ArrayOf** | JSON **array** |
| **Choice, Choice.ID** | JSON **object** with one member. Member key is the integer id converted to string. |
| **Enumerated, Enumerated.ID** | JSON **integer** |
| **Map, Map.ID** | JSON **object**. Member keys are integer ids converted to strings. |
| **MapOf** | JSON **object**. Member keys are integer ids converted to strings. |
| **Record** | JSON **array**. |

## 4. Schema Formats
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)
