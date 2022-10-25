---
title: Verifiable Credentials Hands-On Labs
description: TBC. 
topics:
  - auth0lab
  - verifiable-credentials
  - verifiable-presentations
contentType: how-to
useCase: auth0lab
---
## Overview

We are all used to physical credentials, driver licenses, passports, credit cards, etc. They all have data (claims) made by an issuer (Driver’s License government authority, state department, bank) about a subject. Verifiable credentials (VCs) are digital, cryptographically verifiable versions of these credentials. This means they can be stored on digital devices, and you can use cryptography to verify their validity.

Here are the key parts of a Verifiable Credential:

* __holder:__ the entity that controls the credential, most often this is the subject
* __subject:__ the entity which claims are made about
* __issuer:__ the entity that created the credential
* __claims:__ attributes about the subject that the issuer is asserting
* __proofs (signature):__ Cryptographic mechanism for establishing authorship and validity

### Verifiable Credential Lifecycle

A typical verifiable credential life cycle follows a sequence similar to the following:

1. A user (often the Subject) requests or is given a credential from an Issuer.
2. The Issuer includes data about the Subject in a digital credential, including the Subject's identifier—the Issuer signs the VC with its private key.
3. The user receives the VC and stores it in a digital wallet, becoming the Holder. The digital wallet allows users to store and present VCs of any type.
4. Later, the Holder is using an application that wants to verify the Holder has a particular VC. The Holder uses the digital wallet to present the credential to the Verifier, signing a Verifiable Presentation (VP) with the Holder’s private key.
5. The Verifier cryptographically verifies the VP (it was signed by the Holder and original VC signed by the Issuer) and checks its validity (for example, it hasn't expired). It obtains the holder and Issuer public keys from a Verifiable Data Registry.
6. __(Optional)__ Finally, for any number of reasons the issuer MAY revoke the credential, or the credential MAY expire (e.g. Past an expiration date).

You can find a more in depth explanation and visual presentation of verifiable credentials at [verifiablecredentials.dev](https://verifiablecredentials.dev/).

### Walkthrough Articles

In the following articles, you will experience Verifiable Credentials from the end user and developer perspectives.

* [End User Walkthroughs](/end-user-experience):
  * __Obtain a Credential:__ Using a developer wallet that the Auth0 Lab team has set up, you will obtain a vaccine card from a sample institution.
  * __Present a Credential:__ Using a tool developed by Auth0 Lab to request specific types of credentials, you will request your vaccine card from the developer wallet.
* [Developer Walkthroughs: Issue a Credential using Auth0](/developer-walkthrough-issuance): Using the Auth0 Lab instance of Auth0, you will set up a tenant as a credential issuer.
* [Developer Walkthrough: Verify a Credential using Auth0](/developer-walkthrough-verification): Using the Auth0 Lab instance of Auth0, you will set up a tenant as a credential verifier.

::: note
If you encounter any issues, please raise them to the Auth0 Labs team by heading to our discord [auth0lab.com/chat](https://auth0lab.com/chat).
:::

### Next Steps

1. Visit [verifiablecredentials.dev](https://verifiablecredentials.dev/) to get a quick overview of verifiable credentials with potential use cases.
2. Try the __Walkthrough Articles__.
3. Join the Conversation at [auth0lab.com/chat](https://auth0lab.com/chat).