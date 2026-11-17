---
# <?xml version="1.0" encoding="US-ASCII"?>
# <!DOCTYPE rfc PUBLIC "-//IETF//DTD RFC 2629//EN" "http://xml2rfc.tools.ietf.org/authoring/rfc2629.dtd">
# <?xml-stylesheet type='text/xsl' href='http://xml2rfc.tools.ietf.org/authoring/rfc2629.xslt' ?>
# <!-- NOTE: This MD file is input used to produce the authoritative copy
#     of an OpenID Foundation specification. The authoritative copy is the HTML
#     output. This MD source file is not authoritative. The statement ipr="none"
#     is present only to satisfy the document compilation tool and is not indicative
#     of the IPR status of this specification. The IPR for this specification is
#     described in the "Notices" section. This is a public OpenID Foundation document
#     and not a private document, as the private="..." declaration could be taken
#     to indicate. -->

title: International Government Assurance Profile (iGov) for OAuth 2.0 - draft 10
abbrev: iGov OAuth 2.0
docname: openid-igov-oauth2-1_10
date: '2026-07-25'
category: std
ipr: none
submissiontype: IETF
consensus: true
workgroup: OpenID iGov Working Group
coding: us-ascii
smart-quotes: false
typographic_symbols: false
v: 3
pi:
  tocInclude: 'yes'
  tocdepth: '5'
  symrefs: 'yes'
  sortrefs: 'yes'
  strict: 'yes'
  iprnotified: 'no'
  private: Draft
author:
- name: Kelley Burgin
  initials: K.
  surname: Burgin
  role: editor
  org: The MITRE Corporation
  abbrev: MITRE
  email: kburgin@mitre.org
- name: Tom Clancy
  initials: T.
  surname: Clancy
  role: editor
  org: The MITRE Corporation
  abbrev: MITRE
  email: tclancy@mitre.org
normative:
  OpenID.Core:
    target: http://openid.net/specs/openid-connect-core-1_0.html
    title: OpenID Connect Core 1.0 incorporating errata set 2
    author:
    - name: Nat Sakimura
      initials: N.
      surname: Sakimura
      org: Nomura Research Institute, Ltd.
      abbrev: NRI
    - name: John Bradley
      initials: J.
      surname: Bradley
      org: Ping Identity
      abbrev: Ping Identity
    - name: Michael B. Jones
      initials: M.B.
      surname: Jones
      org: Microsoft
      abbrev: Microsoft
    - name: Breno de Medeiros
      initials: B.
      surname: de Medeiros
      org: Google
      abbrev: Google
    - name: Chuck Mortimore
      initials: C.
      surname: Mortimore
      org: Salesforce
      abbrev: Salesforce
    date: '2023-12-15'
  OpenID.Discovery:
    target: http://openid.net/specs/openid-connect-discovery-1_0.html
    title: OpenID Connect Discovery 1.0 incorporating errata set 2
    author:
    - name: Nat Sakimura
      initials: N.
      surname: Sakimura
      org: Nomura Research Institute, Ltd.
      abbrev: NRI
    - name: John Bradley
      initials: J.
      surname: Bradley
      org: Ping Identity
      abbrev: Ping Identity
    - name: Michael B. Jones
      initials: M.B.
      surname: Jones
      org: Microsoft
      abbrev: Microsoft
    - name: Edmund Jay
      initials: E.
      surname: Jay
      org: IllumilaJSON
      abbrev: Illumila
    date: '2023-12-15'
  OpenID.iGov:
    target: https://openid.net/specs/openid-igov-openid-connect-1_0.html
    title: International Government Assurance Profile (iGov) for OpenID Connect 1.0
    author:
    - name: Michael Varleyy
      initials: M.
      surname: Varley
    - name: Paul Grassi
      initials: P.
      surname: Grassi
    date: '2023-08-03'
  NISTPQC:
    target: https://csrc.nist.gov/projects/post-quantum-cryptography
    title: Post-Quantum Cryptography
    author:
    - org: ''
    date: 2025-12
  ECDHE.MLKEM:
    target: https://datatracker.ietf.org/doc/draft-ietf-tls-ecdhe-mlkem/
    title: Post-quantum hybrid ECDHE-MLKEM Key Agreement for TLSv1.3
    author:
    - name: Kris Kwiatkowski
      initials: K.
      surname: Kwiatkowski
    - name: Panos Kampanakis
      initials: P.
      surname: Kampanakis
    - name: Bas Westerbaan
      initials: B.
      surname: Westerbaan
    - name: Douglas Stebila
      initials: D.
      surname: Stebila
    date: '2025-11-23'
  pkce-vs-nonce:
    target: https://danielfett.de/2020/05/16/pkce-vs-nonce-equivalent-or-not/
    title: 'PKCE vs. Nonce: Equivalent or Not?'
    author:
    - name: Daniel Fett
      initials: D.
      surname: Fett
    date: '2020-05-16'
  browser-based-apps:
    target: https://datatracker.ietf.org/doc/html/draft-ietf-oauth-browser-based-apps
    title: OAuth 2.0 for Browser-Based Applications
    author:
    - name: Aaron Parecki
      initials: A.
      surname: Parecki
    - name: David Waite
      initials: D.
      surname: Waite
    - name: Philippe De Ryck
      initials: P.
      surname: De Ryck
    date: '2025-12-04'
  RFC2119:
  RFC6749:
  RFC6750:
  RFC6797:
  RFC6819:
  RFC6973:
  RFC7009:
  RFC7515:
  RFC7516:
  RFC7517:
  RFC7519:
  RFC7523:
  RFC7591:
  RFC7636:
  RFC7662:
  RFC7638:
  RFC7800:
  RFC8414:
  RFC8252:
  RFC8705:
  RFC8725:
  RFC8996:
  RFC9068:
  RFC9325:
  RFC9364:
  RFC9449:
  RFC9470:
  RFC9700:
  RFC9728:
  RFC9864:

--- abstract

The OAuth 2.0 protocol framework defines a mechanism to allow a resource owner to delegate access to
a protected resource for a client application.

This specification profiles the OAuth 2.0 protocol framework to increase baseline security, provide
greater interoperability, and structure deployments in a manner specifically applicable, but not
limited to consumer-to-government deployments.

--- middle

# Introduction {#Introduction}

This document profiles the OAuth 2.0 web authorization framework for use in the context of securing
web-facing application programming interfaces (APIs), particularly Representational State Transfer
(RESTful) APIs. The OAuth 2.0 specifications accommodate a wide range of implementations with
varying security and usability considerations, across different types of software clients. The OAuth
2.0 client, protected resource, and authorization server profiles defined in this document serve two
purposes:

1. Define a mandatory baseline set of security controls suitable for a wide range of government use
   cases, while maintaining reasonable ease of implementation and functionality
2. Identify optional, advanced security controls for sensitive use cases where increased risk
   justifies more stringent controls.

The companion iGov OpenID Connect profile {{OpenID.iGov}} specifies
additional requirements for federated authentication and the exchange
of end-user identity information using OpenID Connect.

## Requirements Notation and Conventions {#rnc}

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT",
"RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as
described in {{RFC2119}}.

All uses of [JSON Web Signature (JWS)](#RFC7515) and [JSON Web Encryption (JWE)](#RFC7516) data
structures in this specification utilize the JWS Compact Serialization or the JWE Compact
Serialization; the JWS JSON Serialization and the JWE JSON Serialization are not used.

## Terminology {#Terminology}

This specification uses the terms "Access Token", "Authorization Code", "Authorization Endpoint",
"Authorization Grant", "Authorization Server", "Client", "Client Authentication", "Client
Identifier", "Client Secret", "Grant Type", "Protected Resource", "Redirection URI", "Refresh
Token", "Resource Owner", "Resource Server", "Response Type", and "Token Endpoint" defined by
[OAuth 2.0](#RFC6749) , the terms "Claim Name", "Claim Value", and "JSON Web Token (JWT)" defined by
[JSON Web Token (JWT)](#RFC7519) , and the terms defined by [OpenID Connect Core 1.0](#OpenID.Core)
.

## Conformance {#conformance}

This specification defines requirements for the following components:

* OAuth 2.0 clients.
* OAuth 2.0 authorization servers.
* OAuth 2.0 protected resources.

The specification also defines features for interaction between these components:

* Client to authorization server.
* Protected resource to authorization server.

An iGov-compliant component MUST satisfy the requirements applicable to its
role and to the protocol mechanisms it supports or uses. A requirement to
support a mechanism does not require its use in every transaction when this
specification makes that use optional.

Clients, authorization servers, and protected resources MUST use a mutually
supported sender-constraining mechanism for each access token. This profile
permits either mTLS certificate-bound access tokens or DPoP-bound access
tokens; it does not require every component to support both mechanisms.
Components MUST NOT fall back to unconstrained access tokens when a common
sender-constraining mechanism is unavailable.

General-purpose implementations MAY support additional features for
interactions outside this profile. Such support MUST NOT relax the
requirements for interactions conducted under this profile. Interactions
with non-iGov components are outside the scope of this specification.

## Global Requirements {#global-requirements}

iGov implementations SHOULD be crypto-agile, enabling rapid substitution of algorithms and keys so
services remain secure as threats and standards evolve. Implementers of this profile SHOULD monitor
the progress of specifications of post-quantum cryptography.

Connections MUST negotiate TLS 1.2 or a later version. TLS 1.0 and
TLS 1.1 MUST NOT be used, as specified in {{RFC8996}}.  
Each originator of a TLS connection MUST verify the destination's certificate. 
The following TLS 1.2 cipher suites are recommended in Section 4.2
of {{RFC9325}}:

{: empty="true"}
* TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256
* TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384
* TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256
* TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384

When post quantum safety is required for TLS, implementers SHOULD adopt a cipher suite included in
[NIST Post-Quantum Cryptography Standards](#NISTPQC), such as X25519MLKEM768 or SecP256r1MLKEM768,
as specified in [Post-quantum hybrid ECDHE-MLKEM Key Agreement for TLSv1.3](#ECDHE.MLKEM). Of these,
X25519MLKEM768 is broadly supported at the time of writing.

Authorization servers, clients, and resource servers, when creating or processing JWTs

{: empty="true"}
* 1\. MUST adhere to {{RFC8725}}
* 2\. MUST use `PS256`, `ES256`, or `Ed25519` as the JOSE `alg`
  value. The `Ed25519` algorithm identifier is defined in {{RFC9864}}.
* 3\. MUST NOT use or accept the `none` algorithm.

RSA keys MUST have a minimum length of 2048 bits.

Elliptic curve keys MUST have a minimum length of 224 bits.

For the authorization endpoint, the authorization server MAY support
additional TLS 1.2 cipher suites when necessary for browser
interoperability or local regulatory requirements. Such use MUST
conform to the applicable cipher-suite requirements and recommendations
in Section 4 of {{RFC9325}}.

Endpoints for use by web browsers MUST use mechanisms to ensure that connections cannot be
downgraded using TLS Stripping attacks. Protected resources MAY implement an HTTP Strict Transport
Security policy as defined in [HTTP Strict Transport Security (HSTS)](#RFC6797) to mitigate these
attacks. Protected resources SHOULD consider registering web domain names with browsers that offer
browser-side ("preload") HSTS policy enforcement to further mitigate TLS downgrade attacks.

### DPoP Proof Validation and Replay Prevention {#DPoPValidation}

Authorization servers and protected resources processing DPoP requests MUST
perform the applicable proof checks in Section 4.3 of {{RFC9449}}, together
with the requirements for the endpoint receiving the request.

A validator MUST accept proofs only within a bounded validity period. Its
proof-freshness policy MUST document the acceptance window, permitted clock
skew, and any nonce-validity rules that affect that period.

A validator MUST reject reuse of a previously accepted DPoP proof for the
entire period during which that proof would otherwise be accepted,
including permitted clock skew. For this requirement, proof identity is
determined by the DPoP public key's JWK SHA-256 thumbprint, the `jti` value,
and the target URI. Target URI comparison MUST use the same normalization
and exclusion of query and fragment components as the `htu` check in
Section 4.3 of {{RFC9449}}.

A validator MUST NOT accept more than one request carrying the same proof
identity for that target URI during this period. This requirement MUST hold
for concurrent requests and across all processing instances serving the same
logical endpoint. It specifies observable behavior and does not prescribe
a replay-cache design or other implementation architecture.

A valid nonce or an acceptable `iat` value does not, by itself, satisfy
this replay-prevention requirement. Reuse of an access token with a fresh,
otherwise valid proof MUST NOT be rejected merely because the access token
was previously used; all other access-control requirements still apply.

# Client Profiles {#ClientProfiles}

## Client Types {#ClientTypes}

OAuth defines two client types, based on their ability to authenticate securely with the
authorization server

confidential clients:
:   Clients that have credentials with the authorization server.

public clients:
:   Clients without credentials. Public client use cases are out of scope for this profile. An iGov
    Profile for OAuth 2.0 public clients may be developed in the future.

<!-- End of ClientTypes section -->

## Client Type Use Cases {#UseCases}

This specification has been designed around the following client use cases:

web application:
:   A web application is a client running on a web server. Resource owners access the client via an
    HTML user interface rendered in a user agent on the device used by the resource owner. The
    client credentials as well as any access tokens issued to the client are stored on the web
    server and are not exposed to or accessible by the resource owner. In this use case, web
    applications are confidential clients and in-scope for this profile.

native application:
:   A native application is a client installed and executed on the device used by the resource
    owner. Protocol data and credentials are accessible to the resource owner. It is assumed that
    any client authentication credentials included in the application can be extracted. Dynamically
    issued access tokens and refresh tokens can receive an acceptable level of protection. On some
    platforms, these credentials are protected from other applications residing on the same device.
    In this use case, native applications are public clients and out of scope for this profile.
    However, best current practices for native applications are detailed in
    [OAuth 2.0 for Native Apps](#RFC8252). In this use case, native applications are public clients.

browser-based application:
:   A browser-based application is a client in which the client code is downloaded from a web server
    and executes within a user agent (e.g., web browser) on the device used by the resource owner.
    Protocol data and credentials are easily accessible (and often visible) to the resource owner.
    If such applications wish to use client credentials, it is recommended to utilize the backend
    for frontend pattern. Since such applications reside within the user agent, they can make
    seamless use of the user agent capabilities when requesting authorization. In this use case,
    browser-based applications are public clients and out of scope for this profile. However, best
    current practices are detailed in
    [OAuth 2.0 for Browser-Based Applications](#browser-based-apps).

This profile establishes requirements that can only be met by confidential clients. Government
implementers with public client use cases are encouraged to consult the best practices identified
above for those use cases.

## Client Registration {#ClientRegistration}

All clients MUST register with the authorization server. For client software that may be installed
on multiple client instances, each client instance MAY receive a unique client identifier from the
authorization server.

Client registration MAY be completed by either out-of-band configuration or using the
[Dynamic Client Registration Protocol](#RFC7591).

A client registered to obtain mTLS certificate-bound access tokens MUST set
`tls_client_certificate_bound_access_tokens` to the JSON boolean `true` in
its registration metadata. Use of mTLS for client authentication alone does
not require this value to be `true`.

A client registered to obtain DPoP-bound access tokens MUST set
`dpop_bound_access_tokens` to the JSON boolean `true` in its registration
metadata. The corresponding authorization server enforcement requirements
are specified in {{sender-constrained-tokens}}.

Client authentication and access-token sender-constraining are separate
requirements. Clients MUST register the authentication credentials and
metadata appropriate to their selected authentication method, as specified
in {{RequestsToTokenEndpoint}} and {{client-keys}}. Merely using a
certificate to sender-constrain access tokens does not require registering
that certificate's subject DN as a client-authentication identity.

### Redirect URI {#RedirectURI}

Clients using the authorization code grant type MUST register their full redirect URIs.

Clients MUST protect the values passed back to its redirect URI by ensuring that the redirect URI is
one of the following:

* Hosted on a website with Transport Layer Security (TLS) protection (a Hypertext Transfer Protocol
  \- Secure (HTTPS) URI)
* Hosted on a client-specific non-remote-protocol URI scheme (e.g., myapp://)

Clients MUST use a unique redirect URI for each logical authorization server.

Clients MUST NOT forward values passed back to their redirect URIs to other arbitrary or
user-provided URIs (a practice known as an "open redirector").

Refer to [Best Current Practice for OAuth 2.0 Security](#RFC9700) Section 2.4.1 for additional
guidance on implementation of edge cases.

## Sender-constrained Tokens {#PoPTokens}

While a bearer token can be used by anyone in possession of the token, a sender-constrained token is
bound to a particular symmetric or asymmetric key issued to, or already possessed by, the client.
The association of the key to the token is also communicated to the protected resource. When the
client presents the token to the protected resource, it is also required to demonstrate possession
of the corresponding key.

As described in [Best Current Practice for OAuth 2.0 Security](#RFC9700), sender-constrained tokens
could prevent a number of attacks on OAuth that entail the misuse of stolen and leaked access tokens
by unauthorized parties. The attacker would need to obtain the legitimate client's cryptographic key
along with the access token to gain access to protected resources.

All clients MUST use proof of possession to sender-constrain access tokens using either
[OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](#RFC8705) or
[OAuth 2.0 Demonstrating Proof of Possession (DPoP)](#RFC9449).

### DPoP Client Requirements {#DPoPClientRequirements}

Clients using DPoP MUST construct proofs in accordance with Section 4.2 of
{{RFC9449}}. Each request carrying a DPoP proof, including a retry, MUST use
a fresh proof with a new `jti` value. The proof MUST describe the HTTP
method and target URI of that request.

DPoP clients MUST support both the authorization-server nonce mechanism in
Section 8 of {{RFC9449}} and the protected-resource nonce mechanism in
Section 9 of {{RFC9449}}. This includes processing `DPoP-Nonce` response
headers in successful responses and error responses, retaining nonce state
for the issuing server, and using the applicable nonce in subsequent
proofs sent to that server. Clients MUST keep authorization-server and
protected-resource nonce contexts separate and MUST NOT substitute a nonce
issued by one server for a nonce required by another.

Clients MUST support retrying a request after a `use_dpop_nonce` challenge
with a fresh proof containing the supplied nonce. Retrying MUST NOT reuse
the challenged proof or its `jti` value. These client requirements apply
whether or not the servers encountered in a particular deployment elect
to require nonces.

## Authentication Context and Step-Up Authentication Challenge Protocol Support {#AuthNContext}

Clients SHOULD support the mechanism specified in
[OAuth 2.0 Step Up Authentication Challenge Protocol"](#RFC9470) to communicate authentication
context and implement interoperable step up authentication.

This profile acknowledges government use cases will likely operate within an ecosystem of
authentication methods of highly variable security value for the foreseeable future by imposing
requirements to enable protected resources with basic capabilities to communicate requirements for
authentication strength and recency to supporting authorization clients and servers, as well as the
capability to enforce access policies using access tokens augmented with the strength and recency of
the authentication event that led to the issuance of each specific access token.

This profile leverages the supporting server metadata, request, token claims and values, and error
messages from [OAuth 2.0 Step Up Authentication Challenge Protocol](#RFC9470) and
[OpenID Connect Core 1.0](#OpenID.Core).

Digital identity policies and semantic mappings to string values are necessary for implementation
but are out of scope for this profile.

OAuth 2.0 MUST NOT be used as an authentication protocol. Use of the
[OpenID Connect Core 1.0](#OpenID.Core) is RECOMMENDED to provide the identity authentication layer
for iGov OAuth 2.0 delegated access use cases.

## Connection to the Authorization Server {#connection-to-the-authorization-server}

### Requests to the Authorization Endpoint {#RequestsToAuthorizationEndpoint}

All clients MUST use the PKCE S256 code challenge method as described in
[Proof Key for Code Exchange by OAuth Public Clients](#RFC7636) and include the "code\_challenge"
parameter and "code\_challenge\_method", set to "S256", in the authorization request.

Clients making a request to the authorization endpoint MUST use an unpredictable value for the state
parameter with at least 128 bits of entropy. Clients MUST validate the value of the `state`
parameter upon return to the redirect URI and MUST ensure that the state value is securely tied to
the user's current session (e.g., by relating the state value to a session identifier issued by the
client software to the browser).

Clients that have multiple client types MUST have a separate client ID for each client type.

Clients MUST include their full redirect URI in the authorization request.


A client using DPoP MAY bind an authorization code to its DPoP key by
including `dpop_jkt` in the authorization request, as specified in Section
10 of {{RFC9449}}. When pushed authorization requests (PAR) are supported,
the client MAY instead use either binding mechanism in Section 10.1 of
{{RFC9449}}. This profile does not require clients to use authorization-code
binding or to use PAR.

When a client establishes an authorization-code binding, it MUST use the
bound DPoP key in the proof accompanying redemption of that code. If a PAR
request contains both `dpop_jkt` and a DPoP proof, they MUST identify the
same key. Authorization-code binding does not replace PKCE or client
authentication.

The client MAY specify a strength of authentication and maximum age to the authorization server that
should be met when issuing an access token for the requesting client by including parameters in the
authorization request:

acr\_values
:   a space-separated string listing the authentication context class reference values in order of
    preference. The protected resource requires one of these values for the authentication event
    associated with the access token. As defined in Section 1.2 of
    [OpenID Connect Core 1.0&#32;](#OpenID.Core), the authentication context conveys information
    about how authentication takes place (e.g., what authentication method(s) or assurance level to
    meet). It is out of scope of this document to determine how an organization semantically maps
    their digital identity practices to acr values that identify levels of assurance.

max\_age
:   a non-negative integer value that indicates the allowable elapsed time in seconds since the last
    active authentication event associated with the access token.

Furthermore, if the authorization request is a follow-up to a prior request that did not meet the
resource server's initial or subsequent authentication strength or recency requirements, the client
should include the acr\_values and/or max\_age values sent by the resource server with the
insufficient\_user\_authentication error code that specify expected strength and recency requirements
to be provided to the authentication provider, such as the OpenID Provider, in a new authentication
request.

### Requests to the Token Endpoint {#RequestsToTokenEndpoint}

Clients MUST authenticate to the authorization server's token endpoint using either the
private\_key\_jwt method as defined in [OpenID Connect Core](#OpenID.Core) or the
mutually-authenticated transport layer security (mTLS) request method defined in
[OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](#RFC8705).

A client using `private_key_jwt` MUST include a signed `client_assertion`
and the corresponding `client_assertion_type` in the token request, as
specified in {{RFC7523}}. The assertion MUST be signed with the client's
authentication key. The token request itself is not a JWT. A client using
mTLS authentication MUST make the request over a mutually authenticated
TLS connection in accordance with {{RFC8705}}.

A client requesting a DPoP-bound access token MUST include a valid proof
in the `DPoP` HTTP request header field. This applies to each supported
grant type, including `authorization_code`, `refresh_token`, and
`client_credentials`. The proof supplements, and does not replace, the
client-authentication requirements above.

The client MUST verify that a successful response to such a request
identifies the DPoP token type. Otherwise, it MUST discard the response
and MUST NOT use the returned tokens. Refresh-token key-binding requirements
are specified in {{refresh-tokens}}.

If a client uses
[OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](#RFC8705) for
client authentication, exactly one authentication method value MUST be included in the client's
metadata parameters.

tls\_client\_auth
:   Indicates that client authentication to the authorization server will occur with mutual TLS
    utilizing the PKI method of associating a certificate to a client.

self\_signed\_tls\_client\_auth
:   Indicates that client authentication to the authorization server will occur using mutual TLS
    with the client utilizing a self-signed certificate.

A client using the tls\_client\_auth authentication method MUST use exactly one of the below
metadata parameters to indicate the certificate subject value that the authorization server is to
expect when authenticating the respective client:

tls\_client\_auth\_subject\_dn
:   String value specifying the expected subject DN of the client certificate.

tls\_client\_auth\_san\_dns
:   String value specifying the expected dNSName SAN entry in the client certificate.

tls\_client\_auth\_san\_uri
:   String value specifying the expected uniformResourceIdentifier SAN entry in the client
    certificate.

### Client Keys {#client-keys}

Clients using `private_key_jwt` MUST register their authentication public
keys using either `jwks` or `jwks_uri`. The value or referenced document
MUST be a JWK Set as defined in {{RFC7517}}. A `jwks_uri` MUST be reachable
by the authorization server. Use of `jwks_uri` is RECOMMENDED to facilitate
key rotation. These requirements apply to dynamic and out-of-band
registration. A certificate is not required merely because the client
uses `private_key_jwt`.

Clients using `self_signed_tls_client_auth` MUST register certificate
information using `jwks` or `jwks_uri` in accordance with Section 2.2.2 of
{{RFC8705}}, including the required `x5c` representation. Clients using
`tls_client_auth` MUST register the expected certificate identity using
the applicable metadata in {{RequestsToTokenEndpoint}} and Section 2.1.2
of {{RFC8705}}; this method does not require registration of the
certificate through `jwks` or `jwks_uri`.

The authorization server MUST validate registered JWK Sets before using
their keys. DPoP public keys are conveyed in the `jwk` header of DPoP proofs
and need not be registered as client-authentication keys. A valid DPoP
proof does not authenticate the client, and the DPoP key need not be the
client-authentication key.

<!-- End of Client keys -->

<!-- End of Connections to AS section -->

## Connection to the Protected Resource {#connection-to-the-protected-resource}

### Requests to the Protected Resource {#RequestsToProtectedResource}

Clients MUST send access tokens in the `Authorization` HTTP request header
field. DPoP-bound access tokens MUST use the `DPoP` authorization scheme
and MUST be accompanied by a DPoP proof in the `DPoP` header field, as
specified in Section 7.1 of {{RFC9449}}. That proof MUST contain the `ath`
claim for the access token presented in the request.

mTLS certificate-bound access tokens MUST use the `Bearer` authorization
scheme described in Section 2.1 of {{RFC6750}}, together with the mutually
authenticated TLS connection and certificate-binding requirements in
Section 3 of {{RFC8705}}. The client MUST demonstrate possession of the
private key for the certificate to which that access token is bound.

<!-- End of Connections to Protected Resource section -->

<!-- End of Client profile section -->

# Authorization Server Profile {#ServerProfile}

All servers MUST conform to applicable recommendations found in the Security Considerations sections
of {{RFC6749}} and those found in the [OAuth Threat Model Document](#RFC6819).

The authorization server MUST protect all communications to and from its OAuth endpoints using TLS
as described in Section 1.4.

## Connections with clients {#connections-with-clients}

### Grant types {#grant-types}

Authorization servers MUST support the `authorization_code` grant type and MAY support the
`client_credentials` grant type. The implicit grant type MUST NOT be used.

Authorization servers MUST limit each registered client (identified by a client ID) to a single
client type only, since a single piece of software will be functioning at runtime as only one client
type.

### Client authentication {#client-authentication}

Authorization servers MUST authenticate clients using either the private\_key\_jwt method as defined
in [OpenID Connect Core](#OpenID.Core) or the mutually-authenticated transport layer security (mTLS)
request method defined in
[OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](#RFC8705).

For `private_key_jwt`, the authorization server MUST validate the
`client_assertion` and `client_assertion_type` in accordance with
{{RFC7523}}, using the public keys registered for that client. For mTLS
client authentication, it MUST authenticate the client in accordance with
the selected method in Section 2 of {{RFC8705}}.

The authorization server MUST validate redirect URIs for the authorization
code grant against the client's registered redirect URIs.

Client authentication, PKCE validation, and DPoP proof validation are
separate checks. Successful DPoP validation MUST NOT substitute for client
authentication or PKCE validation. DPoP key-binding checks MUST be performed
as specified in {{sender-constrained-tokens}} and {{refresh-tokens}}.

Authorization servers MUST only grant access to higher level scope resources to clients that have
permission to request these scope levels. Authorization servers MUST reject client authorization
requests containing scopes that are outside their permission.

Authorization servers MAY set the expiry time (`exp`) of access\_tokens associated with higher level
resources to be shorter than access\_tokens for less sensitive resources.

Authorization servers MAY allow a `refresh_token` issued at a higher level to be used to obtain an
access\_token for a lower level resource scope with an extended expiry time. The client MUST request
both the higher level scope and lower level scope in the original authorization request. This allows
clients to continue accessing lower level resources after the higher level resource access has
expired \-\- without requiring an additional user authentication/authorization.

When a client requests both a higher level scope and a lower level scope in the original
authorization request, Authorization servers MAY allow refresh tokens issued at the higher level to
be used to obtain an access\_token for a lower level resource scope with an extended expiry time.
This allows clients to continue accessing lower level resources after the higher level resource
access has expired without requiring an additional user authentication/authorization.

### Dynamic Registration {#DynamicRegistration}

Dynamic Registration allows for authorized Clients to on-board programmatically without
administrative intervention. This is particularly important in ecosystems with many potential
Clients, including Mobile Apps acting as independent Clients. Authorization servers MUST support
dynamic client registration, and clients MAY register dynamically using the
[Dynamic Client Registration Protocol](#RFC7591) for authorization code grant types. Authorization
servers MAY limit the scopes available to dynamically registered clients.

Authorization servers MUST protect their Dynamic Registration
endpoints by requiring clients to present credentials that the authorization server would recognize
as authorized participants. Authorization servers MAY accept signed software statements as described
in {{RFC7591}} issued to client software developers from a trusted registration entity. The software
statement can be used to tie together many instances of the same client software that will be run,
dynamically registered, and authorized separately at runtime. When a
software statement is used, it MUST include the following client metadata,
subject to the applicability conditions specified below:

redirect\_uris
:   REQUIRED for clients using the authorization code grant. A JSON array
    of redirect URIs meeting the requirements in {{RedirectURI}}.

grant\_types
:   REQUIRED. A JSON array of grant types used by the client. Values under
    this profile are `authorization_code`, `client_credentials`, and
    `refresh_token`. Clients that use refresh tokens MUST include
    `refresh_token` in addition to the applicable initial grant type.

client\_name
:   REQUIRED. A human-readable name for the client.

client\_uri
:   REQUIRED. The URL of a web page providing information about the client.

token\_endpoint\_auth\_method
:   REQUIRED. The client's authentication method: `private_key_jwt`,
    `tls_client_auth`, or `self_signed_tls_client_auth`. The selected
    method MUST be supported by the authorization server.

tls\_client\_certificate\_bound\_access\_tokens
:   REQUIRED with the JSON boolean value `true` for clients registered to
    obtain mTLS certificate-bound access tokens. This is client metadata,
    not a declaration of authorization-server capabilities.

dpop\_bound\_access\_tokens
:   REQUIRED with the JSON boolean value `true` for clients registered to
    obtain DPoP-bound access tokens, as specified in Section 5.2 of
    {{RFC9449}}.

jwks\_uri or jwks
:   REQUIRED for `private_key_jwt` and `self_signed_tls_client_auth`, with
    contents meeting {{client-keys}}. Clients MUST NOT register both
    parameters. Clients using `tls_client_auth` MUST instead supply the
    applicable certificate-identity metadata described in
    {{RequestsToTokenEndpoint}}.
    
It is NOT RECOMMENDED that authorization servers use IP address or email address to identify
authenticating clients. It is also NOT RECOMMENDED that authorization servers use
tls\_client\_auth\_san\_ip or tls\_client\_auth\_san\_email metadata values

### Client Approval {#ClientApproval}

When prompting the end user with an interactive approval page, the authorization server MUST
indicate to the user:

* Whether the client was dynamically registered, or else statically registered by a trusted
  administrator.
* Whether the client is associated with a software statement, and in which case provide information
  about the trusted issuer of the software statement.
* What kind of access the client is requesting, including scope, protected resources (if applicable
  beyond scopes), and access duration.

For example, if the user believes they are authorizing a very limited type of access, providing the
access level at the consent screen may help the user make informed decisions about sharing sensitive
information.

### Discovery {#Discovery}

The authorization server MUST publish its endpoint locations and
capabilities in a JSON metadata document at the well-known location
specified in Section 3 of {{RFC8414}}. The document MUST satisfy the
applicable requirements of {{RFC8414}} and the metadata requirements
below. Entries identified as conditional are required only when their
stated conditions apply; entries identified as optional remain optional.

issuer
:   The fully qualified issuer URL of the server

authorization\_endpoint
:   The fully qualified URL of the server's authorization endpoint defined by [OAuth 2.0](#RFC6749)

token\_endpoint
:   The fully qualified URL of the server's token endpoint defined by [OAuth 2.0](#RFC6749)

jwks\_uri
:   The HTTPS URL of the authorization server's public JWK Set, as defined
    in {{RFC8414}}. The set MUST contain the public keys needed to validate
    access-token signatures. Registration of client certificates for
    `self_signed_tls_client_auth` is governed by {{client-keys}}, not by
    this authorization-server metadata parameter.

registration\_endpoint
:   The fully qualified URI of the server's URL of the authorization server's
    [OAuth 2.0 Dynamic Client Registration Protocol](#RFC7591) endpoint.

token\_endpoint\_auth\_methods\_supported
:   A JSON array of authentication methods supported by the token endpoint.
    It MUST include at least one of `private_key_jwt`, `tls_client_auth`,
    or `self_signed_tls_client_auth` for use under this profile.

token\_endpoint\_auth\_signing\_alg\_values\_supported
:   REQUIRED when `private_key_jwt` is supported. A nonempty JSON array of
    supported assertion-signing algorithms, in accordance with {{RFC8414}}
    and the algorithm requirements in {{global-requirements}}.

response\_types\_supported
:   A JSON array of supported authorization response types. It MUST include
    `code` for the authorization code flow required by this profile.

grant\_types\_supported
:   A JSON array of supported grant types. It MUST include
    `authorization_code`, and MUST include `refresh_token` when refresh
    tokens are issued and `client_credentials` when that grant is supported.

revocation\_endpoint
:   The fully qualified URL of the server's revocation endpoint defined by
    [OAuth 2.0 Token Revocation](#RFC7009)

introspection\_endpoint
:   The fully qualified URL of the server's introspection endpoint defined in
    [OAuth 2.0 Token Introspection](#RFC7662)

tls\_client\_certificate\_bound\_access\_tokens
:   Boolean value indicating server support for mutual-TLS client certificate-bound access tokens as
    defined in
    [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](#RFC8705). If
    omitted, the default value is false.

mtls\_endpoint\_aliases
:   A JSON object (a map of key-value pairs) containing alternative authorization server endpoints
    that, when present, an OAuth client intending to perform mutual TLS uses in preference to the
    conventional endpoints. Use of this parameter enables isolation of mTLS behavior to only clients
    intending to use mTLS for authentication or sender-constraining tokens. Usage of the parameter
    is specified in
    [OAuth 2.0 Mutual-TLS Client Authentication and Certificate-Bound Access Tokens](#RFC8705)

dpop\_signing\_alg\_values\_supported
:   REQUIRED when DPoP is supported. A nonempty JSON array of JWS algorithm
    identifiers supported for DPoP proofs, as defined in Section 5.1 of
    {{RFC9449}}. Algorithms used under this profile MUST satisfy
    {{global-requirements}}. This parameter has no boolean default value.

acr\_values\_supported
:   OPTIONAL authorization-server metadata describing supported
    authentication context class references, with the meaning specified
    in Section 7 of {{RFC9470}}. This is not client-registration metadata.

Authorization servers MUST support at least one sender-constraining
mechanism permitted by this profile. If
`tls_client_certificate_bound_access_tokens` is `false` or omitted, the
server MUST support DPoP and publish
`dpop_signing_alg_values_supported` as specified above. A server supporting
both mechanisms MUST advertise both capabilities.

If the authorization server is also an OpenID Provider, it MUST publish
OpenID Provider metadata and make its configuration information available
in accordance with Sections 3 and 4 of {{OpenID.Discovery}}.

It is RECOMMENDED that authorization servers provide cache information through HTTP headers and make
the cache valid for at least one week. This allows clients and protected resources to cache the
discovery information.

The authorization server MUST provide its public key in JWK Set format. The key MUST contain the
following fields:

kid
:   The key ID of the key pair used to sign this token

kty
:   The key type

alg
:   The default algorithm used for this key

### Sender-constrained Tokens {#sender-constrained-tokens}

The authorization server MUST issue access tokens bound using the
sender-constraining mechanism selected for the client. It MUST NOT issue
an unconstrained access token under this profile.

When `tls_client_certificate_bound_access_tokens` is `true` in the client's
registration, the authorization server MUST require proof of possession
of the client certificate's private key through mutual TLS and MUST bind
the issued access token to that certificate in accordance with Section 3
of {{RFC8705}}. A TLS connection without the required client-certificate
proof is insufficient.

For a DPoP access-token request, the authorization server MUST process the
request according to Section 5 of {{RFC9449}} and MUST validate the proof
according to {{DPoPValidation}}. When `dpop_bound_access_tokens` is `true`
in the client's registration, a token request without a DPoP proof MUST
be rejected. A successful DPoP request MUST result in an access token
bound to the public key of the validated proof and a response identifying
`DPoP` as the `token_type`. The JWT access token MUST carry the
corresponding `cnf.jkt` value. These requirements apply to all supported
grant types, including refresh-token requests.

Authorization servers supporting DPoP MUST support authorization-code
binding as specified in Section 10 of {{RFC9449}}. Client use is OPTIONAL.
An otherwise valid request MUST NOT be rejected solely because the client
did not establish a DPoP authorization-code binding.

When an authorization code has been bound to a DPoP key, the authorization
server MUST reject redemption unless the token request contains a valid
DPoP proof whose public-key thumbprint matches the binding recorded for
that code. Authorization servers supporting both PAR and DPoP MUST support
both binding mechanisms in Section 10.1 of {{RFC9449}}. If a PAR request
contains both `dpop_jkt` and a DPoP proof identifying different keys, the
request MUST be rejected. This requirement does not mandate PAR support.

The authorization server MAY require a DPoP nonce. When it does, it MUST
follow Section 8 of {{RFC9449}}, including the `DPoP-Nonce` header and the
HTTP 400 `use_dpop_nonce` error response when a required nonce is absent or
unacceptable. Nonce use does not replace {{DPoPValidation}}.

### Revocation {#revocation}

Token revocation allows a client to signal to an authorization server that a given token will no
longer be used.

Authorization servers MUST provide a revocation endpoint URL as specified in
[OAuth 2.0 Token Revocation](#RFC7009) for end users to view a list of clients that have been
granted access to resources on the user's behalf and for end users to revoke this access.

Authorization servers MUST revoke a token if the client requesting the revocation is the client to
which the token was issued, the client has permission to revoke tokens, and the token is able to be
revoked.

Authorization servers MUST NOT allow a client to use a token after it is revoked.

### PKCE {#pkce}

Authorization servers MUST require PKCE for every authorization code flow.
They MUST reject authorization requests without a code challenge and MUST
validate the corresponding code verifier when the code is redeemed, as
specified in {{RFC7636}}.

Authorization servers MUST support the S256 code challenge method. Authorization servers MUST NOT
allow a client to use the plain code challenge method.

The PKCE code\_verifier value MUST contain at least 128 bits of entropy.

PKCE validation MUST be performed independently of client authentication
and any DPoP authorization-code binding. A successful check of one MUST
NOT substitute for either of the others when applicable.

### Redirect URIs {#redirect-uris}

The authorization server MUST validate all redirect URIs for authorization code grant types.

To prevent open redirection and other injection attacks, the authorization server MUST match the
entire redirect URI using an exact string match against registered values and MUST reject requests
with an invalid or missing redirect URI.

### Refresh Tokens {#refresh-tokens}

Authorization servers MAY issue refresh tokens to clients. An authorization
server that issues refresh tokens MUST support the `refresh_token` grant
for their use. Each refresh-token request MUST authenticate the client,
and the authorization server MUST verify that the refresh token was issued
to that client.

For confidential clients, this profile permits additional DPoP key binding
of refresh tokens as a deployment policy. This is an additional restriction
beyond the confidential-client refresh-token behavior described in Section
5 of {{RFC9449}}; it is not required merely because DPoP is used for access
tokens. The binding policy and its key-rotation implications MUST be made
known to the client through registration or deployment configuration.

Refresh tokens MAY be bound to the DPoP key used when they are issued and
MAY remain bound to that original key, including when replacement refresh
tokens are issued through refresh-token rotation. While such a binding is
in effect, the client MUST present a fresh DPoP proof for the bound key
when using the refresh token. The authorization server MUST validate that
proof according to {{DPoPValidation}} and MUST reject the request if the
proof is absent or its public-key thumbprint does not match the binding.
Client authentication remains REQUIRED.

A proof signed by a different key MUST NOT, by itself, cause an existing
refresh-token binding to be replaced or removed. Refresh-token rotation
and DPoP-key rotation are distinct operations. This profile does not define
an in-band mechanism to rebind an existing refresh token to a new DPoP key.

When a refresh token is not DPoP-key-bound, the client MAY use a different
DPoP key in a subsequent refresh request. Subject to the other requirements
of this profile, the authorization server MUST NOT reject that request
solely because the DPoP key differs from one used previously. The newly
issued DPoP-bound access token MUST be bound to the key in the validated
proof accompanying that refresh request.

## Response to Authorization Requests {#response-to-authorization-requests}

Authorization servers respond to an Authorization Request from a client with an Authorization
Response. The following fields MUST be included in the response:

state
:   REQUIRED. The value of the state parameter passed in in the authentication request. This value
    MUST match exactly.

code
:   REQUIRED. The authorization code, a random string issued by the IdP to be used in the request to
    the token endpoint.

PKCE parameters MUST be associated with the authorization code as per Section 4.4 of
[Proof Key for Code Exchange by OAuth Public Clients (PKCE)](#RFC7636).

## JSON Web Tokens (JWT) {#JWTokens}

Authorization servers MUST issue signed, sender-constrained access tokens
in JWT format in accordance with {{RFC9068}}. Protected resources MAY
validate these tokens locally, use token introspection, or combine the two
as specified in {{protected-resource-profile}}. The JWT-format requirement
in this paragraph applies to access tokens; it does not require refresh
tokens to use the same format or claims.

Each JWT access token MUST contain the claims required by {{RFC9068}} and,
at minimum, the following claims required by this profile:

iss
:   The issuer URL of the server that issued the token

client\_id
:   The client id of the client to whom this token was issued

exp
:   The expiration time (integer number of seconds since from 1970-01-01T00:00:00Z UTC), after which
    the token MUST be considered invalid

jti
:   A unique JWT Token ID value with at least 128 bits of entropy. This value MUST NOT be re-used in
    another token.

sub
:   REQUIRED. The subject identifier specified in {{RFC9068}}: the resource
    owner when acting on that owner's behalf, or the client identifier
    when the client acts on its own behalf. End-user identifiers SHOULD
    be pairwise pseudonymous unless the intended audience requires
    otherwise. Privacy considerations do not permit omission of this
    required claim.

aud
:   REQUIRED. A nonempty JSON array identifying the protected resources
    for which the access token is intended. The authorization server MUST
    determine the intended audience before issuing the token, as described
    in Section 3 of {{RFC9068}}. Lack of an explicitly requested resource
    does not permit omission of this claim.

scope
:   The value of the scope claim is a JSON string containing a space-separated list of scopes
    associated with the token, in the format described in Section 3.3 of
    [The OAuth 2.0 Authorization Framework](#RFC6749).

iat
:   The "iat" (issued at) claim identifies the time at which the JWT was issued. This claim can be
    used to determine the age of the JWT. Its value MUST be a number containing a NumericDate value.

cnf
:   REQUIRED. A JSON object identifying the proof-of-possession key or
    certificate to which the access token is bound, using the confirmation
    methods defined in {{RFC7800}}, {{RFC8705}}, and {{RFC9449}}.

    For an mTLS certificate-bound access token, the object MUST contain
    `x5t#S256` with the base64url-encoded SHA-256 digest of the DER-encoded
    client certificate, as specified in Section 3.1 of {{RFC8705}}.

    For a DPoP-bound access token, the object MUST contain `jkt` with the
    base64url-encoded JWK SHA-256 thumbprint of the public key from the
    validated token-request proof, as specified in Section 6.1 of
    {{RFC9449}} and {{RFC7638}}. The authorization-request parameter
    `dpop_jkt` is not an access-token confirmation member.

In order to support backwards compatibility, AS MAY include the azp claim while resource servers
modernize.

The access tokens MUST be signed with [JWS](#RFC7515) . The JWS header MUST contain the following
fields:

kid
:   The key ID of the key pair used to sign this token

Refresh tokens SHOULD be signed with {{RFC7515}} using the authorization
server's access-token signing key. They need not contain the same claims
as access tokens. The authorization server MUST distinguish refresh tokens
from access tokens when validating them, in accordance with {{RFC8725}}.
Any confirmation information in a refresh token MUST represent the actual
refresh-token binding policy in {{refresh-tokens}}, rather than an
assumption that the access-token binding also applies to the refresh token.

The authorization server MAY encrypt access tokens and refresh tokens using [JWE](#RFC7516) .
Encrypted access tokens MUST be encrypted using the public key of the protected resource. Encrypted
refresh tokens MUST be encrypted using the authorization server's public key.

## Token Lifetimes {#TokenLifetimes}

Access tokens SHOULD have a valid lifetime no greater than one hour, and refresh tokens (if issued)
SHOULD have a valid lifetime no greater than twenty-four hours. Specific applications MAY issue
tokens with different lifetimes. Any active token MAY be revoked at any time.

## Scopes {#Scopes}

Scopes define individual pieces of authority that can be requested by clients, granted by resource
owners, and enforced by protected resources. Specific scope values will be highly dependent on the
specific types of resources being protected in a given interface. OpenID Connect, for example,
defines scope values to enable access to different attributes of user profiles.

Authorization servers SHOULD define and document default scope values that will be used if an
authorization request does not specify a requested set of scopes.

To facilitate general use across a wide variety of protected resources, authorization servers SHOULD
allow for the use of arbitrary scope values at runtime, such as allowing clients or protected
resources to use arbitrary scope strings upon registration. Authorization servers MAY restrict
certain scopes from use by dynamically registered systems or public clients.

Refer to {{ClientApproval}} for further information about displaying scopes to end users.

## Connections Between Authorization Servers and Protected Resources {#connections-between-authorization-servers-and-protected-resources}

### Introspection {#introspection}

Token introspection allows a protected resource to obtain access-token
status and metadata from the authorization server over TLS, using the
resource-server authentication requirements below. mTLS is required for
an mTLS authentication method; it is not additionally required merely
because the protected resource uses `private_key_jwt`.

Introspection responses MUST follow {{RFC7662}}. Every response MUST
contain `active`. When `active` is `false`, additional token metadata
SHOULD NOT be returned. When `active` is `true`, this profile requires the
following fields so that the protected resource can validate both the
access token and its sender constraint:

active
:   A JSON boolean indicating whether the token is currently active.

scope
:   The token's granted scopes, represented as a space-separated string.

exp
:   The token's expiration time as a NumericDate value.

sub
:   The subject identifier associated with the token, consistent with the
    access token's `sub` claim.

client\_id
:   The identifier of the client to which the token was issued.

iss
:   The identifier of the authorization server that issued the token.

aud
:   The intended audience, consistent with the access token's `aud` claim.

token\_type
:   `DPoP` for a DPoP-bound access token, or `Bearer` for an mTLS
    certificate-bound access token. The latter value does not remove the
    certificate-binding requirement.

cnf
:   The token's confirmation information: `jkt` for a DPoP-bound access
    token, as specified in Section 6.2 of {{RFC9449}}, or `x5t#S256` for an
    mTLS certificate-bound access token, as specified in Section 3.2 of
    {{RFC8705}}.

The protected resource remains responsible for validating the proof or
client certificate presented with the resource request against this
confirmation information. An `active` value of `true` does not establish
that the requester possesses the bound key. The protected resource MUST
NOT forward the client's resource-request DPoP proof to the introspection
endpoint as a substitute for performing its own proof validation.

Authorization servers MUST require authentication of resource servers for the introspection endpoint
using either private\_key\_jwt or Mutual-TLS methods as described for clients in
{{RequestsToTokenEndpoint}}. Authorization servers MUST NOT allow clients to use token introspection
endpoints.

# Protected Resource Profile {#protected-resource-profile}

## Connections with Clients {#connections-with-clients-2}

Protected resources MUST interpret access tokens using either JWT, token introspection, or a
combination of the two

Protected resources MUST validate access tokens using local JWT validation
in accordance with Section 4 of {{RFC9068}}, authenticated token
introspection in accordance with {{introspection}}, or both. When introspection is used,
the response MUST contain `active` with the value `true` before the token
is accepted. The protected resource MUST establish that the token has a trusted issuer,
has not expired, and includes the protected resource's identifier in its
`aud` value. When both validation methods are used, the protected resource MUST reject
the token if either method indicates that it is invalid.

Protected resources MUST require access tokens in the `Authorization`
HTTP request header field and MUST NOT accept them in query or form
parameters. DPoP-bound tokens MUST use the `DPoP` authorization scheme and
an accompanying `DPoP` proof header. mTLS certificate-bound tokens MUST use
the `Bearer` authorization scheme in Section 2.1 of {{RFC6750}}, together
with the requirements of {{RFC8705}}. A DPoP-bound token presented using
the `Bearer` scheme MUST be rejected.

Protected resources MUST define and document which scopes are required for access to the resource
and any authentication strength or recency requirements for each scope.

For mTLS certificate-bound access tokens, the protected resource MUST
require mutual TLS and MUST verify that the client certificate presented
for the request has the SHA-256 thumbprint identified by `cnf.x5t#S256`,
obtained from the validated access token or authenticated introspection
response. A missing or mismatched certificate MUST cause access to be
denied.

For DPoP-bound access tokens, the protected resource MUST validate the
proof according to {{DPoPValidation}} and Section 7.1 of {{RFC9449}}. It
MUST verify both that the JWK SHA-256 thumbprint of the proof's public key
matches `cnf.jkt` and that the proof's `ath` value matches the hash of the
access token presented in that request. Confirmation information MUST come
from the validated access token or authenticated introspection response.
The protected resource does not validate the authorization-request
parameter `dpop_jkt`.

A protected resource MAY require a DPoP nonce. When it does, it MUST follow
Section 9 of {{RFC9449}}, including the `DPoP-Nonce` header and the HTTP 401
response with a `WWW-Authenticate: DPoP` challenge carrying the
`use_dpop_nonce` error when a required nonce is absent or unacceptable.
Nonce use does not replace {{DPoPValidation}}.

The protected resource MUST deny access unless access-token validation,
sender-constraint validation, and the applicable authorization checks all
succeed.

Protected resources MAY use authentication context or step up authentication to implement access
controls.

If the authentication event associated with the access token does not satisfy the requirements of
the resource server for the given request, the protected resource MUST return a 401 Unauthorized
status code along with a WWW-Authenticate header as defined in
[OAuth 2.0 Step Up Authentication Challenge Protocol](#RFC9470). This header MUST include the
insufficient\_user\_authentication error code to indicate that the presented access token is
inadequate.

Additionally, the response MUST include the acr\_values and/or max\_age auth-params to communicate
the necessary authentication context class reference values and the allowable elapsed time since the
last active authentication event, respectively. The acr\_values parameter should list the required
authentication context class reference values in order of preference, while the max\_age parameter
should indicate the maximum permissible time in seconds since the last user authentication.

The mechanisms by which the protected resource determines whether the authentication requirements
are met are outside the scope of this profile.

Furthermore, protected resources MAY include both acr\_values and max\_age if both are relevant.

Protected resources MAY include the scope parameter if additional scopes are required to access the
resource, as per Section 3.1 of
[The OAuth 2.0 Authorization Framework: Bearer Token Usage](#RFC6750).

## Protecting Resources {#ProtectingResources}

Protected Resources grant access to clients if they present a valid sender-constrained
`access_token` with the appropriate scopes. Resource servers trust the authorization server to
authenticate the end user and client appropriately for the importance, risk, and value level of the
protected resource scope.

Protected resources MAY use [OAuth 2.0 Step Up Authentication Challenge Protocol](#RFC9470) to
implement access controls.

If a protected resources requires a higher end-user authentication trust level to access certain
resources, the protected resource MUST associate those resources with a unique scope and MUST
associate acceptable acr values for each scope as described in
[OAuth 2.0 Step Up Authentication Challenge Protocol](#RFC9470). Protected Resources may also
specify a max\_age for each scope.

Protected resources MAY include the scope parameter if additional scopes are required to access the
resource, as per Section 3.1 of
[The OAuth 2.0 Authorization Framework: Bearer Token Usage](#RFC6750).

## Connections with Authorization Servers {#connections-with-authorization-servers}

Protected resources MUST provide a JWKS URI endpoint to distribute public keys to support signing,
encryption, and authentication to authorization server revocation and introspection endpoints. This
can be achieved by registering the resource server as a client in the AS, and using the mechanism
outlined in section "client authentication". As an alternative mechanism the Resource Server could
implement OAuth 2.0 Protected Resource Metadata {{RFC9728}}. It defines a metadata format that a
client or authorization server can use to obtain the information needed to interact with a protected
resource. This metadata facilitates enhanced interoperability and security including advertisement
and discovery of a protected resource's public key via its jwks\_uri.

Protected resources calling the introspection endpoint MUST use credentials distinct from any other
OAuth client registered at the authorization server.

Protected resources MAY cache the response from the introspection endpoint for a period of time no
greater than half the lifetime of the token. A protected resource MUST NOT accept a token that is
not active according to the response from the introspection endpoint.

Protected resources MUST ensure that the rights associated with the token are sufficient to grant
access to the resource. For example, this can be accomplished by querying the scopes and acr value
associated with the token from the authorization server's token introspection endpoint.

Protected resources MUST limit which authorization servers it will accept valid tokens from. A
resource server MAY accomplish this using a whitelist of trusted servers, a dynamic policy engine,
or other means.

# Security Considerations {#security-considerations}

<!--  Need to add data from John's RFC regarding registration security -->

## DNSSEC Considerations {#dnssec-considerations}

For a comprehensive protection against network attackers, all endpoints should additionally use
[DNSSEC](#RFC9364) to protect against DNS spoofing attacks that can lead to the issuance of rogue
domain-validated TLS certificates.

## Best Practices {#best-practices}

Authorization server, client, and protected resource implementations SHOULD consider including
requirements from [Best Current Practice for OAuth 2.0 Security](#RFC9700),
[JSON Web Token Best Current Practices](#RFC8725) and
[JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens](#RFC9068) that are not explicitly
mentioned in this profile.

## Other Considerations {#other-considerations}

Authorization Servers SHOULD take device posture into account, when possible. Some examples of
device posture include:

* the user's lock screen setting
* the client's level of privilege over the device operating system (e.g. if the client has 'root
  access', the device operating system may be compromised to gain additional privileges not intended
  by the vendor)
* the availability of a device attestation to validate the client

Specific policies or capabilities are outside the scope of this specification.

This profile does not protect against the attacks described in
[The Stronger Attacker Model](#pkce-vs-nonce), in which an attacker could inject the authorization
request and read the authorization response. Although using request object signatures would provide
mitigation, this profile does not require request object signatures because of the lack of available
implementations.

# Privacy Considerations {#privacy-considerations}

This profile addresses the privacy threats identified in
[Privacy Considerations for Internet Protocols](#RFC6973) with normative language throughout the
document. In particular, this profile requires the use of TLS for all network connections, PKCE, and
sender constrained tokens to mitigate the threats in {{RFC6973}}

In OpenID Connect implementations, clients and servers SHOULD implement the privacy threat
mitigations in Section 17 of [OpenID Connect Core 1.0](#OpenID.Core).

--- back

# Acknowledgements {#Acknowledgements}

The OpenID Community would like to thank the following people for their contributions to this
specification: Mark Russel, Mary Pulvermacher, David Hill, Dale Moberg, Adrian Gropper, Eve Maler,
Danny van Leeuwen, John Moehrke, Aaron Seib, John Bradley, Debbie Bucci, Josh Mandel, Sarah
Cecchetti, Giuseppe De Marco, Joseph Heenan, Jim Fenton, Ryan Galluzzo, Bjorn Hjelm, Aaron Parecki,
Michael B. Jones, Stas Mironov, and Andy Regenscheid.

Special thank you to the original iGov Profile editors: Paul Grassi, Justin Richer, and Michael
Varley.

The original version of this specification was part of the Secure RESTful Interfaces project from
The MITRE Corporation, available online at http://secure-restful-interface-profile.github.io/pages/

# Notices {#Notices}

Copyright (c) 2025 The OpenID Foundation.

The OpenID Foundation (OIDF) grants to any Contributor, developer, implementer, or other interested
party a non-exclusive, royalty free, worldwide copyright license to reproduce, prepare derivative
works from, distribute, perform and display, this Implementers Draft, Final Specification, or Final
Specification Incorporating Errata Corrections solely for the purposes of (i) developing
specifications, and (ii) implementing Implementers Drafts, Final Specifications, and Final
Specification Incorporating Errata Corrections based on such documents, provided that attribution be
made to the OIDF as the source of the material, but that such attribution does not indicate an
endorsement by the OIDF.

The technology described in this specification was made available from contributions from various
sources, including members of the OpenID Foundation and others. Although the OpenID Foundation has
taken steps to help ensure that the technology is available for distribution, it takes no position
regarding the validity or scope of any intellectual property or other rights that might be claimed
to pertain to the implementation or use of the technology described in this specification or the
extent to which any license under such rights might or might not be available; neither does it
represent that it has made any independent effort to identify any such rights. The OpenID Foundation
and the contributors to this specification make no (and hereby expressly disclaim any) warranties
(express, implied, or otherwise), including implied warranties of merchantability, non-infringement,
fitness for a particular purpose, or title, related to this specification, and the entire risk as to
implementing this specification is assumed by the implementer. The OpenID Intellectual Property
Rights policy (found at openid.net) requires contributors to offer a patent promise not to assert
certain patent claims against other contributors and against implementers. OpenID invites any
interested party to bring to its attention any copyrights, patents, patent applications, or other
proprietary rights that may cover technology that may be required to practice this specification.

# Document History {#History}

\[\[ To be removed from the final specification \]\]

-10

* Addressed editorial comments by Matt Topper
* Section 2.1: added text to state that a separate iGov OAuth 2.0 Profile for public clients may be
  developed in the future
* Section 1.4: added that RS256 MAY be used for backwards compatibility
* Section 3.1.3: clarified text to prevent Clients from using Dynamic Client Registration in
  high-assurance government environments, even though is it required to be supported by
  Authorization Servers
* Section 2.3: added text from RFC9449 DPoP that every request MUST validate the htm, htu, check for
  replay, and check the dpop\_jkt
* Section 3.3: removed "Clients MUST check for reuse of jti values and reject all tokens issued with
  duplicate jti values." as this may put too much burden on Clients"
* Section 1.4: changed "All network connections MUST be made using TLS 1.3 or above" to "All network
  connections MUST be made using TLS 1.2 or above" to avoid conflicting language
* Sectino 2.7.1: changed "bearer" to "sender constrained"
* Removed examples and fixed typos
* Updated references
* Changed date, version, and document history

-09

* Revised Global Requirements for cryptography to emphasize crypto-agility and align with FAPI
* Revised Post-Quantum guidance with NIST references and ECDHE-MLKEM draft
* Eliminated RS256 requirements throughout and partially updated examples with PS256
* Fixed typos and eliminated redundant or orphaned requirements
* Changed date, version, and document history

-08

* Added description of resource server requirements for authentication context and step-up
* Restructured the document so the text flows better
* Added a method to securely discover or declare JWKS-URI for PR/RS
* Removed public clients to align with FAPI
* Moved requirements to correct section
* Realigned requirements among AS, client, and PR/RS
* Changed date, version, and document history

-06-07

* Addressed comments from WGLC request Jan 31, 2025

-05

* Updated BCP mitigations, aligned with FAPI
* Harmonized cryptography, sender constrained tokens with FAPI
* Added requirement and optionality for authentication context and support for Step-up (RFC 9470)
* Added Privacy Considerations (RFC 6973)
* Added optionality to support enterprise tailoring, especially RFC 8705 mTLS with PKI

-04

* Enable building with https://author-tools.ietf.org/.
* Applied OpenID specification conventions.

-03

* First Implementer's Draft

-2017-06-01

* Aligned with prior version of iGov.
* Added guidance text around using scopes and refresh\_tokens to protect sensitive resources.
* Removed ACR reference.

-2018-05-07

* Imported content from HEART OAuth profile.
