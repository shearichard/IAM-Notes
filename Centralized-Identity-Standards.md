# Centralized Identity Standards

  - SAML (Security Assertion Markup Language)
  - OAuth
  - OIDC - OpenID Connect

# SAML 
An open, Federation Stanard, that supports SSO.

SAML is used to exchange Authentication information IdPs and SPs to verify the user’s identity and permissions, and then grant or deny their access to the applications.

Commonly used by enterprises to allow their users access to both in-house web-applications, and services which they pay for (eg GMail and Salesforce).

An XML based standard transmitted via HTTP (in theory over other transports as well but rarely used).

SAML was developed to support SSO for browser-based applications and services. By contrast because mobile applications are not able to respond to HTTP redirects or POSTS they do not naturally work with SAML, but they can leverage SAML by using a browser/WebView or making use of a SAML-to-OAuth bridge in which the mobile app uses OAuth/OIDC natively but behind the scenes the IdP may authenticate the user using SAML. In a similar way SAML is not a natural fit for authenticating a user to an API, however in a typical scenario, where a mobile app or a browser is the consumer of an API, the user is prompted to login using a browser or a WebView and the app receives a token suitable for API access. The app/browser includes that token in all subsequent calls to the API.

## SAML Mechanics

SAML (Security Assertion Markup Language) is primarily used for web-based Single Sign-On (SSO).

In practice:

    - A user accesses a web application (Service Provider, SP).

    - The SP redirects the browser to the Identity Provider (IdP).

    - The IdP authenticates the user and returns a SAML assertion (an XML document, often Base64-encoded) back to the SP, typically through:

        - HTTP POST binding (form POST)

        - HTTP Redirect binding

        - HTTP Artifact binding


### HTTP Artifact binding
In some situations it may not be desireable to have the entire SAML message pass through the user agent. This can be because

 - The SAML message can be Bulky (hundreds or thousands of characters)

 - Potentially exposed to the user

 - Sometimes inconvenient for systems with strict URL length limits or security policies

When using Artifact binding, instead of the SAML message being passed directly between IdP/SP short identifiers are passed and these are used to allow the IdP and the SP to setup a back channel communication over which the SAML over which the SP can send the *AuthnRequest* and the idP can send the *SAML Response*. This back channel communication is conducted using SOAP over HTTPS.

 all the traffic that passes between the iDp and the SP. In this case *Artifact Binding* can be used.

###  Redirect/POST compared to Artifacts


| HTTP Redirect / HTTP POST     | HTTP Artifacto    |
| --- | --- |
| User → SP: Request protected resource  |   User → SP: Request protected resource |
| SP → UA: Redirect to IdP (or POST form)|  SP → UA: Redirect with Artifact |
| UA → IdP: Sends request via browser   |  UA → IdP: Sends artifact only |
| IdP → UA: Redirect / POST back with SAML assertion |  IdP ↔ SP: SOAP ArtifactResolve/ArtifactResponse |
| UA → SP: Sends SAML assertion     |      UA → SP: Sends response artifact |
| SP: Validate assertion            |       SP ↔ IdP: Resolve artifact to get actual assertion |
| SP: Grant access to user          |       SP: Validate assertion |
