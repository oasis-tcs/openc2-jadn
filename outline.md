## Abstract
JSON Abstract Data Notation (JADN) is an information modeling language. It is based on the CBOR data model (JSON types plus byte string), but JADN types are information-centric rather than data-centric. As with ASN.1, JADN specifications have two parts: abstract type definitions and serialization rules. Type definitions are independent of data format.  Serialization rules define how to represent instances of JADN types using specific data formats such as XML, JSON, or CBOR.

JADN schemas are structured information objects that can be serialized and transferred between applications, displayed in multiple formats such as tables or text-based data definition languages, and translated into concrete schemas for specific data formats.

## 1. Purpose
This document specifies a vocabulary to describe the meaning of structured data, to provide hints for user interfaces working with structured data, and to make assertions about the validity of structured data.
* A schema mechanism to constrain and validate the content of data instances
* Multiple schema documentation formats
* Multiple serialization formats to communicate data instances between applications

## 2. Schema mechanism
A JADN schema is a structured data instance that can be validated, consisting of:
* meta-information about the schema
* type definitions

JADN type definitions provide:
* Value constraints (enumerations, size and value ranges, regex patterns, semantic validation keywords)
* Names for enumerated values and structure fields
* Structure composition styles similar to CDDL
* Serialization options

## 3. Schema Formats
JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

## 4. Serialization
JSON, M-JSON, CBOR, XML
