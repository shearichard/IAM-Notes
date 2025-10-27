# Centralized Identity Standards

  - SAML (Security Assertion Markup Language)
  - OAuth
  - OIDC - OpenID Connect

# SAML 
An open, Federation Stanard, that supports SSO.

Commonly used by enterprises to allow their users access to both in-house web-applications, and services which they pay for (eg GMail and Salesforce).

An XML based standard transmitted via HTTP (in theory over other transports as well but rarely used).


| HTTP Redirect / HTTP POST     | HTTP Artifacto    |
| --- | --- |
| User → SP: Request protected resource  |   User → SP: Request protected resource |
| SP → UA: Redirect to IdP (or POST form)|  SP → UA: Redirect with Artifact |
| UA → IdP: Sends request via browser   |  UA → IdP: Sends artifact only |
| IdP → UA: Redirect / POST back with SAML assertion |  IdP ↔ SP: SOAP ArtifactResolve/ArtifactResponse |
| UA → SP: Sends SAML assertion     |      UA → SP: Sends response artifact |
| SP: Validate assertion            |       SP ↔ IdP: Resolve artifact to get actual assertion |
| SP: Grant access to user          |       SP: Validate assertion |
