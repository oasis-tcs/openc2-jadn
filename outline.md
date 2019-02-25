## Purpose
Using the CBOR application data model (JSON types plus binary string), define:
* A schema mechanism to constrain and validate the content of data instances
* Multiple schema documentation formats
* Multiple serialization formats to communicate data instances between applications

### Schema mechanism
A JADN schema is itself a structured data instance that can be validated.  Includes:
* Value constraints (enumerations, size and value ranges, regex patterns, semantic validation keywords)
* Structure composition styles similar to CDDL

### Schema Formats
JSON, Structure Tables, Data Definition Languages (ASN.1-ish, Thrift-ish, YANG-ish)

### Serialization
JSON, M-JSON, CBOR, XML
