![OASIS Logo](http://docs.oasis-open.org/templates/OASISLogo-v2.0.jpg)
-------

# JSON Abstract Data Notation Specification Version 1.0
## Committee Specification Draft 01
## 01 March 2019
### Specification URIs
#### This version:
* http://docs.oasis-open.org/openc2/jadn/v1.0/csd01/md/jadn-v1.0-csd01.md (Authoritative)
* http://docs.oasis-open.org/openc2/jadn/v1.0/csd01/jadn-v1.0-csd01.html
* http://docs.oasis-open.org/openc2/jadn/v1.0/csd01/jadn-v1.0-csd01.pdf

#### Previous version:

#### Latest version:
* http://docs.oasis-open.org/openc2/jadn/v1.0/jadn-v1.0.md (Authoritative)
* http://docs.oasis-open.org/openc2/jadn/v1.0/jadn-v1.0.html
* http://docs.oasis-open.org/openc2/jadn/v1.0/jadn-v1.0.pdf

#### Technical Committee:
* [OASIS Open Command and Control (OpenC2) TC](https://www.oasis-open.org/committees/openc2/)

#### Chairs:
* Joe Brule (jmbrule@nsa.gov), [National Security Agency](https://www.nsa.gov/)
* Sounil Yu (sounil.yu@bankofamerica.com), [Bank of America](http://www.bankofamerica.com/)

#### Editors:
* David Kemp (dpkemp@radium.ncsc.mil), [National Security Agency](https://www.nsa.gov/)

#### Additional artifacts:
This prose specification is one component of a Work Product that also includes:
* JADN Syntax JSON/JADN schema ([Annex A.2](#a2-jadn-syntax)):
    * http://docs.oasis-open.org/openc2/jadn/v1.0/csd01/schemas/jadn.json
    * http://docs.oasis-open.org/openc2/jadn/v1.0/csd01/schemas/jadn.pdf

#### Abstract:
Cyberattacks are increasingly sophisticated, less expensive to execute, dynamic and automated. The provision of cyberdefense via statically configured products operating in isolation is untenable. Standardized interfaces, protocols and data models will facilitate the integration of the functional blocks within a system and between systems. Open Command and Control (OpenC2) is a concise and extensible language to enable machine to machine communications for purposes of command and control of cyber defense components, subsystems and/or systems in a manner that is agnostic of the underlying products, technologies, transport mechanisms or other aspects of the implementation. It should be understood that a language such as OpenC2 is necessary but insufficient to enable coordinated cyber responses that occur within cyber relevant time. Other aspects of coordinated cyber response such as sensing, analytics, and selecting appropriate courses of action are beyond the scope of OpenC2.

#### Status:
This document was last revised or approved by the OASIS Open Command and Control (OpenC2) TC on the above date. The level of approval is also listed above. Check the "Latest version" location noted above for possible later revisions of this document. Any other numbered Versions and other technical work produced by the Technical Committee (TC) are listed at https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=openc2#technical.

TC members should send comments on this specification to the TC's email list. Others should send comments to the TC's public comment list, after subscribing to it by following the instructions at the "Send A Comment" button on the TC's web page at https://www.oasis-open.org/committees/openc2/.

This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode) Mode of the OASIS IPR Policy, the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page (https://www.oasis-open.org/committees/openc2/ipr.php).

Note that any machine-readable content ([Computer Language Definitions](https://www.oasis-open.org/policies-guidelines/tc-process#wpComponentsCompLang)) declared Normative for this Work Product is provided in separate plain text files. In the event of a discrepancy between any such plain text file and display content in the Work Product's prose narrative document(s), the content in the separate plain text file prevails.

#### Citation format:
When referencing this specification the following citation format should be used:

**[JADN-v1.0]**

_JSON Abstract Data Notation Specification Version 1.0_ - Edited by David Kemp. 1 March 2019. OASIS Committee Specification Draft 01.
http://docs.oasis-open.org/openc2/jadn/v1.0/csd01/jadn-v1.0-csd01.html.
Latest version: http://docs.oasis-open.org/openc2/jadn/v1.0/jadn-v1.0.html.

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
[[TOC]]

-------

# 1 Introduction
OpenC2 is a suite of specifications that enables command and control of cyber defense systems and components.  OpenC2 typically uses a request-response paradigm where a command is encoded by an OpenC2 producer (managing application) and transferred to an OpenC2 consumer (managed device or virtualized function) using a secure transfer protocol. The consumer can respond with status and any requested information.  The contents of both the command and the response are fully defined in schemas, allowing both parties to recognize the syntax constraints imposed on the exchange.

OpenC2 allows the application producing the commands to discover the set of capabilities supported by the managed devices.  These capabilities permit the managing application to adjust its behavior to take advantage of the features exposed by the managed device.  The capability definitions can be easily extended in a noncentralized manner, allowing standard and non-standard capabilities to be defined with semantic and syntactic rigor.

## 1.1 IPR Policy
This specification is provided under the [Non-Assertion](https://www.oasis-open.org/policies-guidelines/ipr#Non-Assertion-Mode) Mode of the [OASIS IPR Policy](https://www.oasis-open.org/policies-guidelines/ipr), the mode chosen when the Technical Committee was established. For information on whether any patents have been disclosed that may be essential to implementing this specification, and any offers of patent licensing terms, please refer to the Intellectual Property Rights section of the TC's web page ([https://www.oasis-open.org/committees/openc2/ipr.php](https://www.oasis-open.org/committees/openc2/ipr.php)).

## 1.2 Terminology
* **Action**: The task or activity to be performed.
* **Actuator**: The entity that performs the action.
* **Command**: A message defined by an action-target pair that is sent from a producer and received by a consumer.
* **Consumer**: A managed device / application that receives commands.  Note that a single device / application can have both consumer and producer capabilities.
* **Producer**: A manager application that sends commands.
* **Response**: A message from a consumer to a producer acknowledging a command or returning the requested resources or status to a previously received request.
* **Target**: The object of the action, i.e., the action is performed on the target.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [[RFC2119](#rfc2119)] and [[RFC8174](#rfc8174)].

## 1.3 Normative References

###### [OpenC2-HTTPS-v1.0]
_Specification for Transfer of OpenC2 Messages via HTTPS Version 1.0_. Edited by David Lemire. Latest version: http://docs.oasis-open.org/openc2/open-impl-https/v1.0/open-impl-https-v1.0.html
###### [OpenC2-SLPF-v1.0]
_Open Command and Control (OpenC2) Profile for Stateless Packet Filtering Version 1.0_. Edited by Joe Brule, Duncan Sparrell, and Alex Everett. Latest version: http://docs.oasis-open.org/openc2/oc2slpf/v1.0/oc2slpf-v1.0.html
###### [RFC768]
Postel, J., "User Datagram Protocol", STD 6, RFC 768, August 1980, http://www.rfc-editor.org/info/rfc768.
###### [RFC791]
Postel, J., "Internet Protocol", RFC 791, September 1981, http://www.rfc-editor.org/info/rfc791.
###### [RFC792]
Postel, J., "Internet Control Message Protocol", STD 5, RFC 792, September 1981, http://www.rfc-editor.org/info/rfc792.
###### [RFC793]
Postel, J., "Transmission Control Protocol", STD 7, RFC 793, September 1981, http://www.rfc-editor.org/info/rfc793.
###### [RFC1034]
Mockapetris, P. V., "Domain names - concepts and facilities", STD 13, RFC 1034, November 1987, http://www.rfc-editor.org/info/rfc1034.
###### [RFC1123]
Braden, R., "Requirements for Internet Hosts - Application and Support", STD 3, RFC 1123, October 1989, http://www.rfc-editor.org/info/rfc1123.
###### [RFC1321]
Rivest, R., "The MD5 Message-Digest Algorithm", RFC 1321, April 1992, http://www.rfc-editor.org/info/rfc1321.
###### [RFC2119]
Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, DOI 10.17487/RFC2119, March 1997, http://www.rfc-editor.org/info/rfc2119.
###### [RFC3986]
Berners-Lee, T., Fielding, R., Masinter, L., "Uniform Resource Identifier (URI): Generic Syntax", STD 66, RFC 3986, January 2005, http://www.rfc-editor.org/info/rfc3986.
###### [RFC4122]
Leach, P., Mealling, M., Salz, R., "A Universally Unique IDentifier (UUID) URN Namespace", RFC 4122, July 2005, http://www.rfc-editor.org/info/rfc4122.
###### [RFC4291]
Hinden, R., Deering, S., "IP Version 6 Addressing Architecture", RFC 4291, February 2006, http://www.rfc-editor.org/info/rfc4291.
###### [RFC4632]
Fuller, V., Li, T., "Classless Inter-domain Routing (CIDR): The Internet Address Assignment and Aggregation Plan", RFC 4632, August 2006, http://www.rfc-editor.org/info/rfc4632.
###### [RFC4648]
Josefsson, S., "The Base16, Base32, and Base64 Data Encodings", RFC 4648, October 2006, http://www.rfc-editor.org/info/rfc4648.
###### [RFC4960]
Stewart, R. "Stream Control Transmission Protocol", RFC 4960, September 2007, http://www.rfc-editor.org/info/rfc4960.
###### [RFC5237]
Arkko, J., Bradner, S., "IANA Allocation Guidelines for the Protocol Field", BCP 37, RFC 5237, February 2008, http://www.rfc-editor.org/info/rfc5237.
###### [RFC5322]
Resnick, P., "Internet Message Format", RFC 5322, October 2008, http://www.rfc-editor.org/info/rfc5322.
###### [RFC5612]
Eronen, P., Harrington, D., "Enterprise Number for Documentation Use", RFC 5612, August 2009, http://www.rfc-editor.org/info/rfc5612.
###### [RFC5952]
Kawamura S., Kawashima M., "A Recommendation for IPv6 Address Text Representation", RFC 5952, August 2010, http://www.rfc-editor.org/info/rfc5952.
###### [RFC6234]
Eastlake 3rd, D., Hansen, T., "US Secure Hash Algorithms (SHA and SHA-based HMAC and HKDF)", RFC 6234, May 2011, http://www.rfc-editor.org/info/rfc6234.
###### [RFC6335]
Cotton, M., Eggert, L., Touch, J., Westerlund, M., Cheshire, S., "Internet Assigned Numbers Authority (IANA) Procedures for the Management of the Service Name and Transport Protocol Port Number Registry", BCP 165, RFC 6335, August 2011, http://www.rfc-editor.org/info/rfc6335.
###### [RFC6838]
Freed, N., Klensin, J., Hansen, T., "Media Type Specifications and Registration Procedures, BCP 13, RFC 6838, January 2013, http://www.rfc-editor.org/info/rfc6838.
###### [RFC7493]
Bray, T., "The I-JSON Message Format", RFC 7493, March 2015, http://www.rfc-editor.org/info/rfc7493.
###### [RFC8174]
Leiba, B., "Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words", BCP 14, RFC 8174, DOI 10.17487/RFC8174, May 2017, http://www.rfc-editor.org/info/rfc8174.
###### [RFC8200]
Deering, S., Hinden, R., "Internet Protocol, Version 6 (IPv6) Specification", RFC 8200, July 2017, http://www.rfc-editor.org/info/rfc8200.
###### [RFC8259]
Bray, T., "The JavaScript Object Notation (JSON) Data Interchange Format", STD 90, RFC 8259, December 2017, http://www.rfc-editor.org/info/rfc8259.
###### [TEXTREP]
Main, A., "Textual Representation of IPv4 and IPv6 Addresses", February 2005, https://tools.ietf.org/html/draft-main-ipaddr-text-rep-02

## 1.4 Non-Normative References
###### [IACD]
M. J. Herring, K. D. Willett, "Active Cyber Defense: A Vision for Real-Time Cyber Defense," Journal of Information Warfare, vol. 13, Issue 2, p. 80, April 2014.<br>Willett, Keith D., "Integrated Adaptive Cyberspace Defense: Secure Orchestration", International Command and Control Research and Technology Symposium, June 2015.

## 1.5 Document Conventions
### 1.5.1 Naming Conventions
* [RFC2119](#rfc2119)/[RFC8174](#rfc8174) key words (see [section 1.4](#14-non-normative-references)) are in all uppercase.
* All property names and literals are in lowercase, except when referencing canonical names defined in another standard (e.g., literal values from an IANA registry).
* All words in structure component names are capitalized and are separated with a hyphen, e.g., ACTION, TARGET, TARGET-SPECIFIER.
* Words in property names are separated with an underscore (_), while words in string enumerations and type names are separated with a hyphen (-).
* The term "hyphen" used here refers to the ASCII hyphen or minus character, which in Unicode is "hyphen-minus", U+002D.
* All type names, property names, object names, and vocabulary terms are between three and 40 characters long.

### 1.5.2 Font Colors and Style
The following color, font and font style conventions are used in this document:

* A fixed width font is used for all type names, property names, and literals.
* Property names are in bold style – **`created_a**t`
* All examples in this document are expressed in JSON. They are in fixed width font, with straight quotes, black text and a light shaded background, and 4-space indentation. JSON examples in this document are representations of JSON Objects. They should not be interpreted as string literals. The ordering of object keys is insignificant. Whitespace before or after JSON structural characters in the examples are insignificant [[RFC8259](#rfc8259)].
* Parts of the example may be omitted for conciseness and clarity. These omitted parts are denoted with the ellipses (...).

Example:

```javascript
{   
    "action": "contain",
    "target": {
        "user_account": {
            "user_id": "fjbloggs",
            "account_type": "windows-local"
        }
    }
}
```

## 1.6 Overview
OpenC2 is a suite of specifications to command actuators that execute cyber defense functions in an unambiguous, standardized way.  These specifications include the OpenC2 Language Specification, Actuator Profiles, and Transfer Specifications.  The OpenC2 Language Specification and Actuator Profile specifications focus on the standard at the producer and consumer of the command and response while the transfer specifications focus on the protocols for their exchange.

* The OpenC2 Language Specification provides the semantics for the essential elements of the language, the structure for commands and responses, and the schema that defines the proper syntax for the language elements that represents the command or response.
* OpenC2 Actuator Profiles specify the subset of the OpenC2 language relevant in the context of specific actuator functions. Cyber defense components, devices, systems and/or instances may (in fact are likely) to implement multiple actuator profiles.  Actuator profiles extend the language by defining specifiers that identify the actuator to the required level of precision and may define command arguments that are relevant and/or unique to those actuator functions.
* OpenC2 Transfer Specifications utilize existing protocols and standards to implement OpenC2 in specific environments. These standards are used for communications and security functions beyond the scope of the language, such as message transfer encoding, authentication, and end-to-end transfer of OpenC2 messages.

The OpenC2 Language Specification defines a language used to compose messages for command and control of cyber defense systems and components.  A message consists of a header and a payload (_defined_ as a message body in the OpenC2 Language Specification Version 1.0 and _specified_ in one or more actuator profiles). 

In general, there are two types of participants involved in the exchange of OpenC2 messages, as depicted in Figure 1-1:

1. **OpenC2 Producers**: An OpenC2 Producer is an entity that creates commands to provide instruction to one or more systems to act in accordance with the content of the command. An OpenC2 Producer may receive and process responses in conjunction with a command.
2. **OpenC2 Consumers**: An OpenC2 Consumer is an entity that receives and may act upon an OpenC2 command.  An OpenC2 Consumer may create responses that provide any information captured or necessary to send back to the OpenC2 Producer. 

The language defines two payload structures:

1. **Command**: An instruction from one system known as the OpenC2 "Producer", to one or more systems, the OpenC2 "Consumer(s)", to act on the content of the command.
2. **Response**: Any information captured or necessary to send back to the OpenC2 Producer  that issued the Command, i.e., the OpenC2 Consumer’s response to the OpenC2 Producer.

![no alt title](images/image_1.png)

**Figure 1-1. OpenC2 Message Exchange**

OpenC2 implementations integrate the related OpenC2 specifications described above with related industry specifications, protocols, and standards. Figure 1 depicts the relationships among OpenC2 specifications, and their relationships to other industry standards and environment-specific implementations of OpenC2. Note that the layering of implementation aspects in the diagram is notional, and not intended to preclude the use of any particular protocol or standard.

![no alt title](images/image_2.png)

**Figure 1-2. OpenC2 Documentation and Layering Model**

OpenC2 is conceptually partitioned into four layers as shown in Table 1-1.

**Table 1-1. OpenC2 Protocol Layers**

| Layer | Examples |
| :--- | :--- |
| Function-Specific Content | Actuator Profiles<br>(standard and extensions) |
| Common Content | Language Specification<br>(this document) |
| Message | Transfer Specifications<br>(OpenC2-over-HTTPS, OpenC2-over-CoAP, …) |
| Secure Transfer | HTTPS, CoAP, MQTT, OpenDXL, ... |

* The **Secure Transfer** layer provides a communication path between the producer and the consumer.  OpenC2 can be layered over any standard transfer protocol.
* The **Message** layer provides a transfer- and content-independent mechanism for conveying requests, responses, and notifications.  A transfer specification maps transfer-specific protocol elements to a transfer-independent set of message elements consisting of content and associated metadata.  
* The **Common Content** layer defines the structure of OpenC2 commands and responses and a set of common language elements used to construct them.
* The **Function-specific Content** layer defines the language elements used to support a particular cyber defense function.  An actuator profile defines the implementation conformance requirements for that function.  OpenC2 Producers and Consumers will support one or more profiles.

## 1.7 Goal
The goal of the OpenC2 Language Specification is to provide a language for interoperating between functional elements of cyber defense systems. This language used in conjunction with OpenC2 Actuator Profiles and OpenC2 Transfer Specifications allows for vendor-agnostic cybertime response to attacks.

The Integrated Adaptive Cyber Defense (IACD) framework defines a collection of activities, based on the traditional OODA (Observe–Orient–Decide–Act) Loop [[IACD](#iacd)]:

* Sensing:  gathering of data regarding system activities
* Sense Making:  evaluating data using analytics to understand what's happening
* Decision Making:  determining a course-of-action to respond to system events
* Acting:  Executing the course-of-action 

The goal of OpenC2 is to enable coordinated defense in cyber-relevant time between decoupled blocks that perform cyber defense functions.  OpenC2 focuses on the Acting portion of the IACD framework; the assumption that underlies the design of OpenC2 is that the sensing/ analytics have been provisioned and the decision to act has been made. This goal and these assumptions guides the design of OpenC2:

* **Technology Agnostic:**  The OpenC2 language defines a set of abstract atomic cyber defense actions in a platform and product agnostic manner
* **Concise:**  An OpenC2 command is intended to convey only the essential information required to describe the action required and can be represented in a very compact form for communications-constrained environments
* **Abstract:**  OpenC2 commands and responses are defined abstractly and can be encoded and transferred via multiple schemes as dictated by the needs of different implementation environments
* **Extensible:**  While OpenC2 defines a core set of actions and targets for cyber defense, the language is expected to evolve with cyber defense technologies, and permits extensions to accommodate new cyber defense technologies.

## 1.8 Purpose and Scope
The OpenC2 Language Specification defines the set of components to assemble a complete command and control message and provides a framework so that the language can be extended. To achieve this purpose, the scope of this specification includes:

1. the set of actions and options that may be used in OpenC2 commands
2. the set of targets and target specifiers
3. a syntax that defines the structure of commands and responses
4. a JSON serialization of OpenC2 commands and responses
5. the procedures for extending the language

The OpenC2 language assumes that the event has been detected, a decision to act has been made, the act is warranted, and the initiator and recipient of the commands are authenticated and authorized. The OpenC2 language was designed to be agnostic of the other aspects of cyber defense implementations that realize these assumptions. The following items are beyond the scope of this specification:

1. Language extensions applicable to some actuators, which may be defined in individual actuator profiles.
2. Alternate serializations of OpenC2 commands and responses.
3. The enumeration of the protocols required for transport, information assurance, sensing, analytics and other external dependencies.

-------

# 2 JADN Definition 
## 2.1 Built-in Types
Data types are defined using an abstract notation that is independent of both their representation within applications ("**API**" values) and their format for transmission between applications ("**serialized**" values).  The data types used in OpenC2 messages are:

| Type | Description |
| :--- | :--- |
| **Primitive Types** |   |
| Binary | A sequence of octets.  Length is the number of octets. |
| Boolean | A logical entity that can have two values: `true` and `false`. |
| Integer | A whole number. |
| Number | A real number. |
| Null | Nothing, used to designate fields with no value. |
| String | A sequence of characters. Each character must have a valid Unicode codepoint.  Length is the number of characters. |
| **Structures** |   |
| Array | An ordered list of unnamed fields. Each field has an ordinal position and a type. |
| ArrayOf(*vtype*) | An ordered list of unnamed fields. Each field has an ordinal position and its value has type *vtype*. |
| Choice | One field selected from a set of named fields. The value has a name and a type. |
| Choice.ID | One field selected from a set of fields.  The API value has an id and a type. |
| Enumerated | A set of named integral constants. The API value is a name. |
| Enumerated.ID | A set of unnamed integral constants. The API value is an id. |
| Map | An unordered set of named fields. Each field has an id, name and type. |
| Map.ID | An unordered set of fields.  The API value of each field has an id and type. |
| Record | An ordered list of named fields, e.g. an OrderedMap, structure, or row in a table. Each field has an ordinal position, name, and type. |

* **API** values do not affect interoperabilty, and although they must exhibit the characteristics specified above, their representation within applications is unspecified.  A Python application might represent the Map type as a dict variable, a javascript application might represent it as an object literal or an ES6 Map type, and a C# application might represent it as a Dictionary or a Hashtable.

* **Serialized** values are critical to interoperability, and this document defines a set of **serialization rules** that unambiguously define how each of the above types are serialized using a human-friendly JSON format.  Other serialization rules, such as for XML, machine-optimized JSON, and CBOR formats, exist but are out of scope for this document.  Both the format-specific serialization rules in Section 3.1.5 and the format-agnostic type definitions in Sections 3.2, 3.3 and 3.4 are Normative.

Types defined with an ".ID" suffix (Choice.ID, Enumerated.ID, Map.ID) are equivalent to the non-suffixed types except:

1. Field definitions and API values are identified only by ID.  The non-normative description may include a suggested name.
2. Serialized values of Enumerated types and keys of Choice/Map types are IDs regardless of serialization format.

OpenC2 type definitions are presented in table format. All table columns except Description are Normative. The Description column is always Non-normative.

For types without individual field definitions (Primitive types and ArrayOf), the type definition includes the name of the type being defined and the definition of that type. This table defines a type called *Email-Addr* that is a *String* that has a semantic value constraint of *email*:

| Type Name | Type Definition | Description |
| :--- | :--- | :--- |
| **Email-Addr** | String (email) | Email address |

For Structure types, the definition includes the name of the type being defined, the built-in type on which it is based, and options applicable to the type as a whole.  This is followed by a table defining each of the fields in the structure.  This table defines a type called *Args* that is a *Map* containing at least one field.  Each of the fields has an integer Tag/ID, a Name, and a Type.  Each field in this definition is optional (Multiplicity = 0..1), but per the type definition at least one must be present.

**_Type: Args (Map) [1..*]_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **start_time** | Date-Time | 0..1 | The specific date/time to initiate the action  |
| 2 | **stop_time** | Date-Time | 0..1 | The specific date/time to terminate the action |
| 3 | **duration** | Duration | 0..1 | The length of time for an action to be in effect |

The field columns present in a structure definition depends on the base type:

| Base Type | Field Definition Columns |
| :--- | :--- |
| Enumerated.ID | ID, Description |
| Enumerated | ID, Name, Description |
| Array, Choice.ID, Map.ID | ID, Type, Multiplicity (#), Description |
| Choice, Map, Record | ID, Name, Type, Multiplicity (#), Description |

The ID column of Array and Record types contains the ordinal position of the field, numbered sequentially starting at 1.  The ID column of Choice, Enumerated, and Map types contains tags with arbitrary integer values. IDs and Names are unique within each type definition.

### 2.1.1 Abstract Types

As stated in Section 3.1.1, all OpenC2 data types are defined abstractly, independently of both how they are represented within an application and how they are communicated between applications.  The critical distinction is that an abstract type represents what an item **is**, not how it is implemented.

Two criteria are used to determine what an item **is**:
1. Is there a *standard* that defines the item, and if so, what does the standard say, and
2. Is the definition *unambiguous*, i.e., how easy is it to determine if an instance of that item is valid.

The IPv4 standard [RFC791] defines what an IPv4 address **is** - a 32 bit number. [TEXTREP], an Internet-Draft that expired in 2005, is the most authoritative definition available for the **"Textual Representation of** IPv4 and IPv6 addresses".

By criterion 1, both documents agree that an IPv4 address is a 32 bit Binary value, not a String, and the abstract definition of IPv4-Address is based on those standards.  And by criterion 2, defining an IPv4 Address to be a 32 bit value is entirely unambiguous - it is trivial to determine if an instance is valid, and there is no disagreement among implementations.  By comparison, determining if a String fits the definition in [TEXTREP] is not as trivial.  The ABNF definition is 7 lines of text that requires a bit of thought to interpret, and most implementations do not follow that ABNF.  The string "129.034.215.162" may or may not be a valid IP address depending on how strictly an implementation adheres to the draft.

By the same logic, an IPv4 address range is not an IPv4 address. The standard "Classless Inter-domain Routing (CIDR): The Internet Address Assignment and Aggregation Plan" [RFC4632] defines what the address range **is**:
> "the "/16" indicating that the mask to extract the network portion of the prefix is a 32-bit value where the most
   significant 16 bits are ones and the least significant 16 bits are zeros."

and how it is **shown** in CIDR notation:
> "a 4-octet quantity followed by the "/" (slash) character, followed by a decimal value between 0 and 32".

The abstract definition of an address range is the two parts defined by the standard. The serialization rule "Array.ipv4-net" says that it is transmitted between applications as a single string in CIDR notation.  Neither the type definition nor the serialization rule say anything about how implementations represent IPv4 address ranges internally - they may use strings or other variables or structures or classes as determined by their developers.

**_Type: IPv4-Net (Array.ipv4-net)_**

| ID | Type | # | Description |
| :--- | :--- | :--- | :--- |
| 1 | IPv4-Addr | 1 | ipv4-address - as defined in RFC 4632 Section 3.1 |
| 2 | Integer | 0..1 | CIDR prefix-length.  If omitted, refers to a single host address. |


### 2.1.2 Semantic Value Constraints
Structural validation alone may be insufficient to validate that an instance meets all the requirements of an application. Semantic validation keywords specify value constraints for which an authoritative definition exists.

| Keyword | Applies to Type | Constraint |
| :--- | :--- | :--- |
| **email** | String | Value must be an email address as defined in RFC 5322, section 3.4.1 |
| **hostname** | String | Value must be a hostname as defined in RFC 1034 section 3.1 |
| **uri** | String | Value must be a Uniform Resource Identifier (URI) as defined in RFC 3986 |
| **eui** | Binary | Value must be an EUI-48 or EUI-64 as defined in EUI |

### 2.1.3 Multiplicity
Property tables for types based on Array, Choice, Map and Record include a multiplicity column (#) that specifies the minimum and maximum cardinality (number of elements) of a field.  As used in the Unified Modeling Language ([UML](#uml)), typical examples of multiplicity are:

| Multiplicity | Description | Keywords |
| :--- | :--- | :--- |
| 1 | Exactly one instance | Required |
| 0..1 | No instances or one instance | Optional |
| 1..* | At least one instance | Required, Repeatable |
| 0..* | Zero or more instances | Optional, Repeatable |
| m..n | At least m but no more than n instances | Required, Repeatable |

When used with a Type, multiplicity is enclosed in square brackets, e.g.,:

| Type Name | Base Type | Description |
| :--- | :--- | :--- |
| **Features** | ArrayOf(Feature) [0..10] | An array of zero to ten names used to query an actuator for its supported capabilities. |

### 2.1.4 Derived Enumerations
An Enumerated field may be derived ("auto-generated") from the fields of a Choice, Map or Record type by appending ".*" to the type name.

**_Type: Example-sel (Record)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | targets | Target.* | 1..* | Enumeration auto-generated from a Choice |

### 2.2 Imported Types
Each Actuator profile defines a *base schema* - the subset of the OpenC2 language relevant in the context of specific actuator functions.  Each profile has a unique name used to unambiguously identify the profile document (and it's base schema).

In addition, a profile may define profile-specific types that are *imported* by its base schema. Type definitions are imported under a *namespace* to allow profiles to be developed independently and their definitions brought together into a single merged schema without risk of ambiguity or name collisions. A namespace consists of:

* The unique name of the schema being imported
* A short namespace identifier (**nsid**) assigned locally within the base schema to refer to the unique name

In this document, type definitions are represented as tables and importing is a conceptual process.  When using a schema language, importing is an actual process that takes a base schema and a set of imported schemas as inputs and produces a single merged schema as output. In both cases the base schema locally assigns a namespace identifier to each schema that it imports, and importing a schema means prepending the namespace identifier to all type names defined in that schema.

Producers and Consumers MUST support the syntax defined by the merged schema, regardless of whether the implementation is based on conceptually merging tables from a set of documents or physically merging a set of schema files.

**Example - Import a Schema**

Assume that a schema being imported includes the following type definitions:

**_Type: Target (Choice)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **device** | Device | 1 | |

**_Type: Device (Map)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **model** | String | 0..1 | |
| 2 | **manufacturer** | String | 0..1 | |

After conceptually importing that schema under the "abc" namespace identifier, the base schema would be interpreted as if it contained the following definitions:

**_Type: abc:Target (Choice)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **device** | abc:Device | 1 | |

**_Type: abc:Device (Map)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **model** | String | 0..1 | |
| 2 | **manufacturer** | String | 0..1 | |

A Consumer lists the profiles it supports in response to the "query features imports" command. The Producer then knows the unique names of all imported profiles and the nsids assigned to each profile by that Consumer. The Target type defined in the profile's base schema contains a subset of the Target fields defined in this document, plus a field for each imported profile:

**_Type: Target (Choice)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **artifact** | Artifact | 1 | An array of bytes representing a file-like object or a link to that object. |
| 3 | **device** | Device | 1 | The properties of a hardware device. |
| 7 | **domain_name** | Domain-Name | 1 | A network domain name. |
| 1030 | **abc** | abc:Target | 1 | Imported targets defined in the "abc" profile |

The **device** target and the **abc** target have different Types, and even though the combined schema includes type definitions for both Device and abc:Device, those definitions do not conflict.

The ID and Name of a field whose Type is imported are arbitrary, but because there may not be a way for a Producer to determine the schema used by a Consumer, the field Name assigned to an imported type SHOULD equal the nsid of that type. 

# 3 Serialization
| OpenC2 Data Type | JSON Serialization Requirement |
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
| Choice.ID | JSON **object** with one member. Member key is the integer field id converted to string. |
| **Enumerated** | JSON **string** |
| **Enumerated.ID** | JSON **integer** |
| **Map** | JSON **object**. Member keys are field names. |
| **Map.ID** | JSON **object**. Member keys are integer field ids converted to strings. |
| **Record** | JSON **object**. Member keys are field names. |

## 3.1 ID and Name Serialization
Instances of Enumerated types and keys for Choice and Map types are serialized as ID values except when using serialization formats intended for human consumption, where Name strings are used instead.  Defining a type using ".ID" appended to the base type (e.g., Enumerated.ID, Map.ID) indicates that:

1. Type definitions and application values use only the ID.  There is no corresponding name except as an optional part of the description.
2. Instances of Enumerated values and Choice/Map keys are serialized as IDs regardless of serialization format.

## 3.2 Integer Serialization
For machine-to-machine serialization formats, integers are represented as binary data, e.g., 32 bits, 128 bits.   But for human-readable serialization formats (XML and JSON), integers are converted to strings.  For example, the JSON "number" type represents integers and real numbers as decimal strings without quotes, e.g., { "height": 68.2 }, and as noted in RFC 7493 Section 2.2, a sender cannot expect a receiver to treat an integer with an absolute value greater than 2^^53 as an exact value.

The default representation of Integer types in text serializations is the native integer type for that format, e.g., "number" for JSON.   Integer fields with a range larger than the IEEE 754 exact range (e.g., 64, 128, 2048 bit values) are indicated by appending ".<bit-size>" or ".*" to the type, e.g. Integer.64 or Integer.*.  All serializations ensure that large Integer types are transferred exactly, for example in the same manner as Binary types.  Integer values support arithmetic operations; Binary values are not intended for that purpose.



#### 3.3.2.1 OpenC2 Response Status Code
**_Type: Status-Code (Enumerated.ID)_**

| ID | Description |
| :--- | :--- |
| 102 | **Processing** - an interim response used to inform the producer that the consumer has accepted the request but has not yet completed it. |
| 200 | **OK** - the request has succeeded. |
| 301 | **Moved Permanently** - the target resource has been assigned a new permanent URI. |
| 400 | **Bad Request** - the consumer cannot process the request due to something that is perceived to be a producer error (e.g., malformed request syntax). |
| 401 | **Unauthorized** - the request lacks valid authentication credentials for the target resource or authorization has been refused for the submitted credentials. |
| 403 | **Forbidden** - the consumer understood the request but refuses to authorize it. |
| 404 | **Not Found** - the consumer has not found anything matching the request. |
| 500 | **Internal Error** - the consumer encountered an unexpected condition that prevented it from fulfilling the request. |
| 501 | **Not Implemented** - the consumer does not support the functionality required to fulfill the request. |
| 503 | **Service Unavailable** - the consumer is currently unable to handle the request due to a temporary overloading or maintenance of the consumer. |




# 4 Schema Syntax
**4.1 Schema**

**_Type: Schema (Record)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **meta** | Meta | 1 | Information about this schema module |
| 2 | **types** | Type | 1..n | Types defined in this schema module |

### 4.1.1 Meta
Meta-information about this schema

**_Type: Meta (Map)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **module** | Uname | 1 | Unique name |
| 2 | **title** | String | 0..1 | Title |
| 3 | **version** | String | 0..1 | Patch version (module includes major.minor version) |
| 4 | **description** | String | 0..1 | Description |
| 5 | **imports** | Import | 0..n | Imported schema modules |
| 6 | **exports** | Identifier | 0..n | Data types exported by this module |
| 7 | **bounds** | Bounds | 0..1 | Schema-wide upper bounds |

#### 4.1.1.1 Import
**_Type: Import (Array)_**

| ID | Type | # | Description |
| :--- | :--- | :--- | :--- |
| 1 | Nsid | 1 | **nsid** - A short local identifier (namespace id) used within this module to refer to the imported module |
| 2 | Uname | 1 | **uname** - Unique name of the imported module |

#### 4.1.1.2 Bounds
Schema-wide default upper bounds.   If included in a schema, these values override codec default values but are limited to the codec hard upper bounds. Sizes provided in individual type definitions override these defaults.

**_Type: Bounds (Array)_**

| ID | Type | # | Description |
| :--- | :--- | :--- | :--- |
| 1 | Integer | 1 | **max_msg** - Maximum serialized message size in octets or characters |
| 2 | Integer | 1 | **max_str** - Maximum text string length in characters |
| 3 | Integer | 1 | **max_bin** - Maximum binary string length in octets |
| 4 | Integer | 1 | **max_fields** - Maximum number of elements in ArrayOf |

### 4.1.2 Type
Definition of a data type.

**_Type: Type (Array)_**

| ID | Type | # | Description |
| :--- | :--- | :--- | :--- |
| 1 | Identifier | 1 | **tname** - Name of this data type |
| 2 | JADN-Type.* | 1 | **btype** - Base type. Enumerated value derived from the list of JADN data types. |
| 3 | Option | 1..n | **topts** - Type options |
| 4 | String | 1 | **tdesc** - Description of this data type |
| 5 | JADN-Type.&2 | 1..n | **fields** - List of fields for compound types.  Not present for primitive types. |

#### 4.1.2.1 JADN Type
Field definitions applicable to the built-in data types (primitive and compound) used to construct a schema.

**_Type: JADN-Type (Choice)_**

| ID | Name | Type | # | Description |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Binary | Null |   | Octet (binary) string |
| 2 | Boolean | Null |   | True or False |
| 3 | Integer | Null |   | Whole number |
| 4 | Number | Null |   | Real number |
| 5 | Null | Null |   | Nothing |
| 6 | String | Null |   | Character (text) string |
| 7 | Array | FullField |   | Ordered list of unnamed fields |
| 8 | ArrayOf | Null |   | Ordered list of fields of a specified type |
| 9 | Choice | FullField |   | One of a set of named fields |
| 10 | Enumerated | EnumField |   | One of a set of id:name pairs |
| 11 | Map | FullField |   | Unordered set of named fields |
| 12 | Record | FullField |   | Ordered list of named fields |

#### 4.1.2.2 Enum Field
Item definition for Enumerated types

**_Type: EnumField (Array)_**

| ID | Type | # | Description |
| :--- | :--- | :--- | :--- |
| 1 | Integer | 1 | Item ID |
| 2 | Identifier | 1 | Item name |
| 3 | String | 1 | Item description |

#### 4.1.2.3 Full Field
Field definition for compound types Array, Choice, Map, Record

**_Type: FullField (Array)_**

| ID | Type | # | Description |
| :--- | :--- | :--- | :--- |
| 1 | Integer | 1 | Field ID or ordinal position |
| 2 | Identifier | 1 | Field name |
| 3 | Identifier | 1 | Field type |
| 4 | Options | 1 | Field options.  This field is an empty array (not omitted) if there are none. |
| 5 | String | 1 | Field description |

#### 4.1.2.4 Identifier
| Type Name | Base Type | Description |
| :--- | :--- | :--- |
| **Identifier** | String | A string beginning with an alpha character followed by zero or more alphanumeric | underscore | dash characters, max length 32 characters |

#### 4.1.2.5 Nsid
| Type Name | Base Type | Description |
| :--- | :--- | :--- |
| **Nsid** | String | Namespace ID - a short identifier, max length 8 characters |

#### 4.1.2.6 Uname
| Type Name | Base Type | Description |
| :--- | :--- | :--- |
| **Uname** | String | Unique name (e.g., of a schema) - typically a set of Identifiers separated by forward slashes |

#### 4.1.2.7 Options
| Type Name | Base Type | Description |
| :--- | :--- | :--- |
| **Options** | ArrayOf(Option) | An array of zero to ten option strings. |

#### 4.1.2.8 Option
| Type Name | Base Type | Description |
| :--- | :--- | :--- |
| **Option** | String | An option string, minimum length = 1.  The first character is the option id.  Remaining characters if any are the option value. |

-------

# 5 Conformance

-------
