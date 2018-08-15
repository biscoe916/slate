---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json--example
  - json--schema

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:

search: true
---

# Elevator Pitch
### TDF3 is...

**For** SMBs and Enterprises 

**Who** want to protect their files 

**The** TDF3 architecture  

**Is** a backwards compatible set of specifications, and libraries

**That** allows for advanced data protection and granular access control

**Unlike** TDF2, TDF3 allows for offline create, streaming large files, and multi-party data ownership. It will also be open-source.

# Schemas

## manifest.json

### Summary
TODO: Write a summary of what the manifest json is here.

```json--example
// Example
{
  "payload": {
    "type": "reference",
    "url": "0.payload",
    "protocol": "zip",
    "isEncrypted": true
  },
  "encryptionInformation": {
    "type": "split",
    "keyAccess": [
      {
        "type": "remoteWrapped",
        "url": "http:\/\/kas.gsk.com:5000",
        "protocol": "kas",
        "wrappedKey": "OqnOETpwyGE3PVpUpwwWZoJTNW24UMhnXIif0mSnqLVCUPKAAhrjeue11uAXWpb9sD7ZDsmrc9ylmnSKP9vWel8ST68tv6PeVO+CPYUND7cqG2NhUHCLv5Ouys3Klurykvy8\/O3cCLDYl6RDISosxFKqnd7LYD7VnxsYqUns4AW5\/odXJrwIhNO3szZV0JgoBXs+U9bul4tSGNxmYuPOj0RE0HEX5yF5lWlt2vHNCqPlmSBV6+jePf7tOBBsqDq35GxCSHhFZhqCgA3MvnBLmKzVPArtJ1lqg3WUdnWV+o6BUzhDpOIyXzeKn4cK2mCxOXGMP2ck2C1a0sECyB82uw==",
        "policyBinding": "BzmgoIxZzMmIF42qzbdD4Rw30GtdaRSQL2Xlfms1OPs=",
        "encryptedMetadata": "ZoJTNW24UMhnXIif0mSnqLVCU="
      }
    ],
    "method": {
      "algorithm": "aes-256-gcm",
      "streamable": false,
      "iv": "S5FtOSsesp3VfzfNHcHQpg==",
    },
    "integrityInformation":{
      "hashes": []
    },
    "policy": "eyJib2R5IjogeyJkYXRhQXR0cmlidXRlcyI6IFt7InVybCI6ICJodHRwczovL2V4YW1wbGUuY29tL2F0dHIvQ2xhc3NpZmljYXRpb24uUyIsICJuYW1lIjogIlRvcCBTZWNyZXQifSwgeyJ1cmwiOiAiaHR0cHM6Ly9leGFtcGxlLmNvbS9hdHRyL0NPSS5QUlgiLCAibmFtZSI6ICJQcm9qZWN0IFgifV19fQ=="
  }
}
```

```json--schema
// Full JSON-Schema
{
  "$id": "https://virtru.com/schemas/tdf.json",
  "$schema": "https://json-schema.org/draft-07/schema#",
  "title": "TDF Manifest",
  "description": "A manifest file containing data about the TDF.",
  "type": "object",
  "required": [
    "payload",
    "encryptionInformation"
  ],
  "properties": {
    "payload": { 
      "$ref": "#/definitions/payload"
    },
    "encryptionInformation": {
      "$ref": "#/definitions/encryptionInformation"
    }
  },
  "maxProperties": 2,
  "definitions": {
    "payload": {
      "description": "Contains metadata for the TDF's payload",
      "type": "object",
      "properties": {
        "type": {
          "description": "TODO: Will can you fill this in?",
          "type": "string"
        },
        "url": {
          "description": "TODO: Will can you fill this in?",
          "type": "string"
        },
        "protocol": {
          "description": "TODO: Will can you fill this in?",
          "type": "string"
        },
        "isEncrypted": {
          "description": "Boolean designating whether or not the payload is encrypted",
          "type": "boolean"
        }
      }
    },
    "encryptionInformation": {
      "description": "Top level element for holding information related to the encryption of an assertion or payload. Also contains information about how to derive a key. ",
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "description": "Information describing the encryption scheme.",
          "enum": [
            "split",
            "shamir"
          ]
        },
        "keyAccess": {
          "description": "TODO: Will can you fill this in?",
          "type": "array",
          "items":{
            "$ref": "https://virtru.com/schemas/key-access-object.json"
          }
        },
        "method": {
          "description": "Object describing the encryption method",
          "type": "object",
          "properties": {
            "streamable": {
              "type": "boolean",
              "description": "The type of method used for encryption. Chunked vs. a single chunk payload"
            },
            "algorithm": {
              "description": "The encryption algorithm used to encrypt the payload",
              "type": "string",
              "examples": [
                "aes-256-gcm"
              ]
            },
            "iv": {
              "description": "Base64 intialization vector",
              "type": "string"
            }
          },
          "required": [
            "algorithm",
            "iv"
          ]
        },
        "integrityInformation": {
          "type": "object",
          "description": "Object contaiting information required to validate payload integrity. ",
          "properties": {
            "hashes": {
              "type": "array",
              "items": {
                "type": "string",
                "description": "Hashes for the individual chunks of the payload in the event the payload was built using a streaming/chunked approach"
              }
            }
          }
        },
        "policy": {
          "description": "A base64 encoded version of the policy object. The policy object is defined here:: https://virtru.com/schemas/tdf-policy-object.json",
          "type": "string"
        }
      }
    }
  }
}
```
### payload
Parameter | Type | Description
--------- | -- | -----------
payload | Object |Contains metadata for the TDF's payload. Including type, url, protocol and isEncrypted. TODO: FILL IN MORE HERE
payload.type | String | TODO: Still need to figure out what this is
payload.url | String |  What is the name of the protocol file in the TDF.
payload.protocol | String |  Designates whidch protocol was used. Currently, only ZIP is supported.
payload.isEncrypted | Boolean |  Designates whether or not the payload is encrypted

### encryptionInformation
Parameter | Type | Description
--------- | -- | -----------
encryptionInformation | Object | Contains information describing the method of encryption. As well as information about one or more KASes which own the TDF. 
encryptionInformation.type | String | The type of scheme used for accessing keys, and providing authorization to the payload. The schema supports multiple options, but currently the only option supported by our libraries is `split`.
encryptionInformation.keyAccess | Array |  An array of keyAccess Objects. Defined in the next section below.
encryptionInformation.method | Object | An object which describes the information required to actually decrypt the payload once the key is retrieved. Includes the algorithm, and iv at a minimum.
encryptionInformation.method.algorithm | String | The algorithm used for encryption. ie. `aes-256-gcm`
encryptionInformation.method.isStreamable | boolean | isStreamable designates whether or not a TDF payload is streamable. If it's streamable, the payload is broken into chunks, and indivdual hashes are generated per chunk to establish integrity of the individual chunks.
encryptionInformation.method.iv | String | The initialization vector for the encrypted payload.

### keyAccessObject

The keyAccessObject is defined in its own section [below](#keyaccessobject-2).

### integrityInformation
Parameter | Type | Description
--------- | -- | -----------
integrityInformation | Object | An object which allows an application to validate the integrity of the payload. Or a chunk of a payload should it be a streamable TDF.
integrityInformation.hashes | Array | An array of hashes TODO: Will can you fill this in? Zack asked specifically about how the hash is generated.

### policy
Parameter | Type | Description
--------- | -- | -----------
policy | String | The policy object which has been JSON stringified, then base64 encoded. The policy object is described in the next section.

## keyAccessObject

### Summary
A summary of the key access object

```json--example
  {
    "type": "remoteWrapped",
    "url": "http:\/\/kas.gsk.com:5000",
    "protocol": "kas",
    "wrappedKey": "OqnOETpwyGE3PVpUpwwWZoJTNW24UMhnXIif0mSnqLVCUPKAAhrjeue11uAXWpb9sD7ZDsmrc9ylmnSKP9vWel8ST68tv6PeVO+CPYUND7cqG2NhUHCLv5Ouys3Klurykvy8\/O3cCLDYl6RDISosxFKqnd7LYD7VnxsYqUns4AW5\/odXJrwIhNO3szZV0JgoBXs+U9bul4tSGNxmYuPOj0RE0HEX5yF5lWlt2vHNCqPlmSBV6+jePf7tOBBsqDq35GxCSHhFZhqCgA3MvnBLmKzVPArtJ1lqg3WUdnWV+o6BUzhDpOIyXzeKn4cK2mCxOXGMP2ck2C1a0sECyB82uw==",
    "policyBinding": "BzmgoIxZzMmIF42qzbdD4Rw30GtdaRSQL2Xlfms1OPs=",
    "encryptedMetadata": "ZoJTNW24UMhnXIif0mSnqLVCU="
  }
```

```json--schema 
{
  "$id": "https://virtru.com/schemas/tdf.json",
  "$schema": "https://json-schema.org/draft-07/schema#",
  "title": "Key access object",
  "description": "TODO: Will can you fill this in?",
  "type": "object",
  "required": [
    "type",
    "url",
    "protocol",
    "wrappedKey",
    "policyBinding",
    "metadataKek",
    "encryptedMetadata"
  ],
  "properties": {
    "type": {
      "type": "string",
      "description": "TODO: Will can you fill this in?",
      "examples": [
        "remoteWrapped"
      ]
    },
    "url": {
      "type": "string",
      "description": "URL pointing to the KAS",
      "examples": [
        "https:\/\/kas.gsk.com:5000"
      ]
    },
    "protocol": {
      "type": "string",
      "description": "Protocol being used for this split.",
      "examples": [
        "kas"
      ]
    },
    "wrappedKey": {
      "type": "string",
      "description": "The base64 wrapped key used to encrypt the payload"
    },
    "policyBinding": {
      "type": "string",
      "description": "Base64 Signature of the policy. Signed using the public key of the KAS."
    },
    "encryptedMetadata": {
      "type": "string",
      "description": "Metadata for the policy which has been encrypted, then base64 encoded",
      "examples": [
        "R5IjogeyJkY=="
      ]
    }
  }
}

```

Parameter | Type | Description
--------- | -- | -----------
keyAccessObject | Object | TODO: Fill this in
type | String | TODO: Will, what are some other options here?
url | String | A url pointing to the KAS 
protocol | String | Protocol being used. Currently only KAS is supported
wrappedKey | String | The symetric key used to encrypt the payload. It has been encrypted using the public key of the KAS, then base64 encoded.
policyBinding | String | TODO: Can you fill this in
encryptedMetadata | String | Metadata associated with the TDF, and the request. The contents of the metadata are freeform, and are used to pass information from the client, and any plugins that may be in use by the KAS. For example, in Virtru's scenario, we could include information about things like, watermarking, expiration, and also data about the request. Things like clientString, could also be placed here.


## Policy Object

### Summary
The policy object is an object generated by the client at the time of the payload's encryption. It contains information required for the KAS to make an access decision, such as, `dataAttributes`, and `dissem`. The policyObject is stored in the manifest.json for a TDF, and sent to the KAS along with an entity object so that the KAS may make an access decision. 

A KAS, by default, is stateless, but by using plugins, may sync the policy data received from an access request using a datastore of its choice. It's up to the developer of a plugin to determine how that data is stored in their store, but it's recommended they choose something like outlined in the schema so as to simply the adapter logic in the plugin.

```json--schema
{
  "$id": "https://virtru.com/schemas/policy.json",
  "$schema": "https://json-schema.org/draft-07/schema#",
  "title": "TDF Policy object",
  "description": "Policy for the TDF. Includes attributes, and encrypted metadata for the KAS",
  "type": "object",
  "required":[
    "uuid",
    "body"
  ],
  "properties": {
    "uuid": {
      "type": "string",
      "description": "A UUID for the policy, generated by the client which created the TDF",
      "examples": [
        "630086f5-f238-4cd1-897c-0a7bd4da6f66"
      ]
    },
    "body": {
      "type": "object",
      "description": "TODDO: Fill this in",
      "properties": {
        "dataAttributes": {
          "type": "array",
          "description": "Attributes associated with the policy. Used by KAS to make access decisions",
          "items": {
            "type": "object",
            "description": "An attribute object",
            "properties": {
              "url": {
                "type": "string",
                "description": "A url pointing to an attribute's policy",
                "examples":[
                  "https:\/\/example.com\/attr\/Classification.TS"
                ]
              },
              "name": {
                "type": "string",
                "description": "The name of the attribute",
                "examples":[
                  "Top Secret"
                ]
              }
            }
          }
        }
      },
      "required": [
        "dataAttributes"
      ]
    },
    "dissem": {
      "type": "array",
      "description": "An array of userIds to be given access to the TDF content",
      "items": {
        "type": "string",
        "description": "A userID, most likely an email",
        "examples": [
          "johndoe@virtru.com"
        ]
      }
    }
  }
}
```

```json--example
{
"uuid": "1111-2222-33333-44444-abddef-timestamp",
"body": {
    "dataAttributes": [
      {
        "url": "https:\/\/example.com\/attr\/Classification.S",
        "name": "Top Secret"
      },
      {
        "url": "https:\/\/example.com\/attr\/COI.PRX",
        "name": "Project X"
      }
    ],
    "dissem": [
      "user-id@domain.com"
    ]
  }
}
```
### uuid
Parameter | Type | Description
--------- | -- | -----------
uuid | String | A unique UUID for the TDF's policy.

### body
Parameter | Type | Description
--------- | -- | -----------
body | Object | Object which contains information about the policy required for the KAS to make an access decision. 
body.dataAttributes | Array | An array of dataAttributes. dataAttributes are defined in the next sub-section.
body.dissem | Array | An array of unique userIds. It's used to explicitly list users/entities that should be given access to the payload.