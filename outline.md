## 1. Purpose
Using the CBOR application data model (JSON types plus binary string), define:
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
