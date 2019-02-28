## Abstract
JSON Abstract Data Notation (JADN) is an information modeling language. It is based on the CBOR data model (JSON types plus byte string), but JADN types are information-centric rather than data-centric. JADN specifications have two parts: abstract type definitions that are independent of data format, and serialization rules that define how to represent an instance of a type in a specific data format such as XML, JSON, or CBOR.

A JADN schema is a structured information object that can be serialized and transferred between applications, displayed in multiple documentation formats such as tables and text-based data definition languages, and translated into concrete schemas for specific data formats.

## Non-Normative References

###### [TEXTREP]
*"Textual Representation of IPv4 and IPv6 Addresses"*, https://tools.ietf.org/html/draft-main-ipaddr-text-rep-02#section-3.1

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
This section is Non-Normative.

RFC 3444 describes differences between information models (IMs) and data models (DMs):
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

Information refers to *what* needs to be communicated between applications, and data is *how* that information
is represented when communicating.  More formally, information theory defines information as the unexpected data or
"entropy" contained in a message.  When information is serialized for transmission in a canonical format, the additional
data used for purposes such as text conversion, delimiting and framing contains zero entropy because it is known a priori.
If the serialization is non-canonical, any additional entropy introduced into the data during serialization
(e.g., whitespace) is discarded on deserialization.

For example, in an Information model an IPv4 address ([RFC791]) is a 32 bit value because it contains 32 bits of
information that an application cares about. Data Models define how an IPv4 address is serialized, for example:
* IPv4 Dotted Octet Format [TEXTREP] contained in a JSON string: "192.168.141.240" (17 bytes / 136 bits of data).
* Hex value contained in a JSON string: "C0A88DF0" (10 bytes / 80 bits)
* CBOR byte string: 0x44c0a88df0 (5 bytes / 40 bits).

The data is different when using different DMs, but the information in these three examples is the same.

## 3. JADN Types

JADN type definitions provide:
* Value constraints (enumerations, size and value ranges, regex patterns, semantic validation keywords)
* Names for enumerated values and structure fields
* Structure composition styles similar to CDDL
* Serialization options

## 4. Schema Formats
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

## 5. Serialization
JSON, M-JSON, CBOR, XML
