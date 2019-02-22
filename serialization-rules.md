## 3 Serialization
JADN type definitions are agnostic of any particular serialization format. Three formats are defined here; additional formats are possible.

### 3.1 JSON Serialization

The following JSON serialization rules are used to represent JADN data types in human-friendly format, where:
1) Records are serialized as objects
2) Object keys are serialized as meaningful strings
3) Binary values such as IP addresses are serialized using type-specific text representations

| JADN Type | JSON Serialization Requirement |
| :--- | :--- |
| **Binary** | JSON **string** containing Base64url encoding of the binary value as defined in Section 5 of RFC 4648. |
| **Binary.x** | JSON **string** containing Base16 (hex) encoding of a binary value as defined in Section 8 of RFC 4648. Note that the Base16 alphabet does not include lower-case letters. |
| **Binary.ipv4-addr** | JSON **string** containing the text representation of an IPv4 address as specified in Section 3 of "Textual Representation of IPv4 and IPv6 Addresses" [TEXTREP]. |
| **Binary.ipv6-addr** | JSON **string** containing the text representation of an IPv6 address as specified in Section 4 of RFC 5952. |
| **Boolean** | JSON **true** or **false** |
| **Integer** | JSON **number** |
| **Number** | JSON **number** |
| **Null** | JSON **null** |
| **String** | JSON **string** |
| **Array** | JSON **array** |
| **Array.ipv4-net** | JSON **string** containing the text representation of an IPv4 address range as specified in Section 3.1 of RFC 4632. |
| **Array.ipv6-net** | JSON **string** containing the text representation of an IPv6 address range as specified in Section 2.3 of RFC 4291. | 
| **ArrayOf** | JSON **array** |
| **Choice** | JSON **object** with one member.  Member key is the field name.   |
| **Choice.ID** | JSON **object** with one member. Member key is the integer field id converted to string. |
| **Enumerated** | JSON **string** |
| **Enumerated.ID** | JSON **integer** |
| **Map** | JSON **object**. Member keys are field names. |
| **Map.ID** | JSON **object**. Member keys are integer field ids converted to strings. |
| **Record** | JSON **object**. Member keys are field names. |

### 3.2 CBOR Serialization

When using Concise Binary Object Representation [CBOR] serialization, instances of JADN datatypes
are serialized using the following  types.  CBOR type #x.y = Major type x, Additional information y.

* All suffixes to Binary and Array types used for human-friendly serialization (e.g., Binary.x) are ignored.
* The .ID suffix on Choice, Enumerated and Map types is ignored.

Names for CBOR types are as shown in Concise Data Definition Language [CDDL].  For structure types, arrays and maps are
the only two representation formats, but they are used to specify four distinguishable styles of composition:
* **vector**, an array of elements that have the same semantics.
* **record**, an array the elements of which have different, positionally defined semantics, as detailed in the data structure definition.
* **table**, a map from a domain of map keys to a domain of map values that have the same semantics.
* **struct**, a map from a domain of map keys as defined by the specification to a domain of map values that have semantics bound to the map key.

| JADN Type | CBOR Serialization Requirement |
| :--- | :--- |
| **Binary** | **bstr**: a byte string (#2). |
| **Boolean** | **bool**: a Boolean value (False = #7.20, True = #7.21). |
| **Integer** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Number** |  **float64**: IEEE 754 Double-Precision Float (#7.27). |
| **Null** | **null**: (#7.22) |
| **String** | **tstr**: a text string (#3). |
| **Array** | **record**: an array of data items (#4). |
| **ArrayOf** | **vector**: an array of data items (#4). |
| **Choice** | **struct**: a map (#5) containing one pair. First item is the tag, second item is the value. |
| **Enumerated** | **int**: an unsigned integer (#0) or negative integer (#1) |
| **Map** | **struct**: a map (#5) of pairs. In each pair, first item is an integer tag, second item is the value. |
| **Record** | **record**: an array of data items (#4). |

### 3.3 M2M JSON Serialization Requirements:

The following JSON serialization rules are used to represent JADN data types in a compact format optimized for machine-to-machine communication, where:
1) Records are serialized as arrays
2) Object keys are serialized as integer tags in string format
3) Binary values are serialized in Base64url format

M2M JSON serialization is equivalent to CBOR serialization using CDDL's JSON preface ([CDDL] Appendix E).
* All suffixes to Binary and Array types used for human-friendly serialization (e.g., Binary.x) are ignored.
* The .ID suffix on Choice, Enumerated and Map types is ignored.

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
| **Choice** | JSON **object** with one member. Member key is the integer field id converted to string. |
| **Enumerated** | JSON **integer** |
| **Map** | JSON **object**. Member keys are integer tags converted to strings. |
| **Record** | JSON **array**. |
