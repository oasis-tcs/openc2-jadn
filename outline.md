## Abstract
JSON Abstract Data Notation (JADN) is an information modeling language. It is based on the CBOR data model (JSON types plus byte string), but JADN types are information-centric rather than data-centric. As with ASN.1, JADN specifications have two parts: abstract type definitions and serialization rules. Type definitions are independent of data format.  Serialization rules define how to represent instances of JADN types using specific data formats such as XML, JSON, or CBOR.

JADN schemas are structured information objects that can be serialized and transferred between applications, displayed in multiple formats such as tables or text-based data definition languages, and translated into concrete schemas for specific data formats.

## Non-Normative References

###### [MDA]
*"The Fast Guide to Model Driven Architecture"*, https://www.omg.org/mda/mda_files/Cephas_MDA_Fast_Guide.pdf

###### [RFC3444]
*"On the Difference between Information Models and Data Models"*, https://tools.ietf.org/html/rfc3444


## 1. Purpose
This document specifies a vocabulary to describe the meaning of structured data, to provide hints for user interfaces working with structured data, and to make assertions about the validity of structured data.
* A schema mechanism to constrain and validate the content of data instances
* Multiple schema documentation formats
* Multiple serialization formats to communicate data instances between applications

## 2. Information vs. Data
This non-normative section provides rationale and context for JADN.
### 2.1 Information Models
RFC 3444 describes differences between information models (IMs) and data models (DMs):
* The main purpose of an IM is to model managed objects at a conceptual level,
independent of any specific implementations or protocols used to transport
the data. In order to make the overall design as clear as possible, an IM
should hide all protocol and implementation details.
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
### 2.2 Model Driven Architecture
In Model Driven Architecture [MDA], the IM is part of a Platform Independent Model (**PIM**) and DMs
are used in Platform Specific Models (**PSM**), where:
* A PIM exhibits a sufficient degree of independence so as to enable its
mapping to one or more platforms. This is commonly achieved by defining a set of
services in a way that abstracts out technical details.
* A PSM combines the specifications in the PIM with the details
required to stipulate how a system uses a particular type of platform. 
### 2.3 Abstracting Information
Information theory defines *information* as the amount of unexpected data, or "entropy", contained in a message.
An IM defines just the information (unexpected data) in a message, while DMs based on serialization rules add
greater or lesser amounts of expected data (containing no information) in order to format the information
for transmission. If the serialization is canonical it adds no unexpected data; if not, all unexpected data
added during serialization is discarded on deserialization.

That theoretical description has practical implications when designing information models:
1) if there are multiple equivalent representations of an item, the shortest is **always** that item's information.
2) bookkeeping data (such as string lengths, item separators, and framing data) is **never** information.

Deciding what constitutes an IM is illustrated through examples.
* Heuristic:
    * Authoritative definition
    * Unambiguous definition
    * Information theory

## 3. Schema mechanism
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JADN type definitions provide:
* Value constraints (enumerations, size and value ranges, regex patterns, semantic validation keywords)
* Names for enumerated values and structure fields
* Structure composition styles similar to CDDL
* Serialization options

## 4. Schema Formats
JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

## 5. Serialization
JSON, M-JSON, CBOR, XML
