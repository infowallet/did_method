# InfoWallet DID Method Specification

## Abstract
 InfoWallet is a credential system that operates on a block-chain ensured by each other node and does not require a central controller. 
It is a credential system that achieves both security and convenience decentralization by DPKI and Verifiable Claim.

## OverView
In the InfoWallet system, several types of certificates are issued. Decentralized ID is used as the identifier of the certificate.
Also, the public key required for encryption for secure exchange of certificates and personal information is also solved through DID.


## InfoWallet DID Method Name

The namestring that shall identify this DID method is: iwt


## InfoWallet DID Format

iwt-did   = "did:iwt:" id-string 
id-string = 1* idchar
idchar    = 1-9 / A-H / J-N / P-Z / a-k / m-z 

Example
did:iwt:4EFNaYeA9hDp6F55JAB38EFtNcYEbbM9nwKr

## Operation
DID Operation provides SmartContract of InfoWallet BlockChain in the form of REST API to access.
/ did_create /did_create_simple / did_read / did_update / did_delete and / did_verify to perform signature validation within SmartContract

### Create

Create a DID_Document in json format and send it to / did_create uri
Request DID creation. SmartContract returns true if it has not already been issued to the block chain.
In addition, at the time of creation, proof must pass the signature verification in the block chain.
The key used in the Create Proof must also be included in the Authentication.

Example
Simple Request data 1

endport : /did_create_simple
input : did , publicKey , signature
output : result

{
"id": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn",
"publicKey": ["677AgijZXPuwmhSVMTkNXGArgMY7GA9iyhrMj8gs","3DzeDRdey97pWydGAuKGEWZKpBzjevwGB4NbyZPkkVs4RoF"],
"signature" : "5nbzWuDGXyb...FPg6HmZ4JM6q=="
}

Response data	
{
"result": true,
"message" : "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn created"
}
```

```
endport : /did_create
input : did_document
output : result

{
"id": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn",
  "publicKey": [{
    "id": "did: iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn #keys-1",
    "type": "EcdsaKoblitzSignature2016",
    "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
  }, {
    "id": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn#keys-2",
    "type": "EcdsaKoblitzSignature2016",
     "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
  }
  ],
  "authentication": [{
    "publicKey": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn #keys-1"
  } 
  ],
}
"proof": {
    "type": " EcdsaKoblitzSignature2016",
    "created": "2018-08-02T16:01:10Z",
	"nonce" : "dQew214232".
    "creator": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn#keys-1",
    "signatureValue": "Ee2.....=="
}

Response data	
{
"result": true,
"message" : "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn created"
}
```

### Read 
Anyone can read DID_Document with did

endport : /did_read
input : did
output : did_document

input
{
"id": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn"
}

output
{
"id": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn",
  "publicKey": [{
    "id": "did: iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn #keys-1",
    "type": "EcdsaKoblitzSignature2016",
    "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
  }, {
    "id": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn#keys-2",
    "type": "EcdsaKoblitzSignature2016",
     "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
  }
  ],
  "authentication": [{
    "publicKey": "did:iwt:7V2FnzCykod7aK9eMBEtKEdyfxSwn #keys-1"
  } 
  ]
}

### Update

endport : /did_update
input : did_document (included proof)
output : did_document

### Delete

endport : /did_delete
input : did,proof
output : did_document



# References
## [1]. W3C Decentralized Identifiers (DIDs) v0.11, https://w3c-ccg.github.io/did-spec/.
