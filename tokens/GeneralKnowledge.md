# Tokens General Knowledge

## What Is A Token?
Tokens are pieces of data that carry just enough information to facilitate the process of determining a user's identity or authorizing a user to perform an action. All in all, tokens are artifacts that allow application systems to perform the authorization and authentication process.

The main difference between JWTs and opaque tokens is that an unencrypted JWT can be interpreted by anybody that holds the token, whereas opaque tokens cannot.

## Clasified by form: JWT Tokens and Opaque Tokens

### JWT Token:

An unencrypted JWT consists of three parts: a header, a payload, and a signature. The header contains the name of the token type and the signing algorithm used for the signature. The payload, which is the contents of the token, is encoded but not encrypted, so anybody can read it. The signature makes sure that the payload is not tampered with. There are [examples of encoded and decoded JWTs] available that you can experiment with to learn more.

A JWT is a JSON string that contains all the claims and information it represents and is certified by a signature from the issuer. By default, it’s unencrypted, but it can be encrypted via the JSON Web Encryption (JWE) standard.

### Opaque Token:

Opaque tokens cannot be read by people that hold them since they are undecodable strings. A client cannot read the contents of the token without interacting with the authorization server by querying an introspection endpoint or checking the claims of the token with the userinfo endpoint.

An opaque token's format is chosen by the issuer of the token. Usually, it's a string of numbers and/or characters that identifies some information in the database of the issuer. This is in contrast to JWTs where the holder of the token can't inspect it without contacting the issuer (ie the contents are opaque).

## Clasified by purpose: Access Tokens (OAuth 2.0) and ID Tokens (OpenID Connect)

### Access Token:

Credential that can be used by an application to access an API. It informs the API that the bearer of the token has been authorized to access the API and perform specific actions specified by the scope that has been granted. An Access Token can be in any format, but two popular options include opaque strings and JSON Web Tokens (JWT). They should be transmitted to the API as a Bearer credential in an HTTP Authorization header.

Los Identity Providers generan Access Tokens, para controlar el consumo de sus servicios:
In addition, if you have chosen to allow users to log in through an Identity Provider (IdP), such as Facebook, the IdP will issue its own access token to allow your application to call the IDP's API. For example, if your user authenticates using Facebook, the access token issued by Facebook can be used to call the Facebook Graph API. These tokens are controlled by the IdP and can be issued in any format. See Identity Provider Access Tokens for details.

OAuth 2.0 doesn’t prescribe a specific format for access tokens, so you can use opaque tokens, JWT, or any other format that satisfies the necessary properties.

### ID Token:

ID tokens are tokens that a server issues to prove that the user is authenticated. You can use them to log into third-party services with another service that acts as an identity provider, like Google.
The OpenID Connect protocol requires you to use JWTs for ID tokens.

### Refresh Token:

Special kind of token that can be used to obtain a renewed Access Token. It is useful for renewing expiring Access Tokens without forcing the user to log in again. Using the Refresh Token, you can request a new Access Token at any time until the Refresh Token is blocklisted.

The client application can get a new access token as long as the refresh token is valid and unexpired. Consequently, a refresh token that has a very long lifespan could theoretically give infinite power to the token bearer to get a new access token to access protected resources anytime. The bearer of the refresh token could be a legitimate user or a malicious user. 

## Introspection Endpoint:

The token introspection endpoint needs to be able to return information about a token
OAuth 2.0 token introspection defines a method that allows authorized protected resources to query the authorization server to determine the set of metadata for a given token (access token, authorization code, or a refresh token) that was presented to them by an OAuth client.
Based on the metadata of the particular token, it allows the resource server to consume the protected resource,
This metadata includes:
- Whether the token is currently active (or if it has expired or otherwise been revoked)
- The rights of accessing the token carries (usually conveyed through OAuth 2.0 scopes)
- The authorization context in which the token was granted (including who authorized the token and which client it was issued to)

## Possible states for:

### Authorization codes:

ACTIVE- Valid and yet to be exchanged for an access token
INACTIVE- Invalid and already being exchanged for an access token
EXPIRED- Invalid as it got expired before being exchanged to an access token

### Access tokens:

ACTIVE- Valid access token. Although the state is ACTIVE, the timestamp calculation may reveal it to be EXPIRED, but this happens only during the first access token request or token validation request after expiration.
INACTIVE- Refreshed using refresh_token grant type before expiration. Also, this state is used in cases when users and userstores are deleted, user passwords are updated, etc.
EXPIRED- Invalid and expired access token. Refresh token can still be valid though.
REVOKED- Revoked access token. Refresh token also gets revoked along with access token. Access token could have been in ACTIVE or EXPIRED state while revoking.

# In the Identity Server:

The OAuth introspection endpoint is: https://<IS_HOST>:<IS_PORT>/oauth2/introspect

The Callback Url is the exact location in the service provider's application to which an access token will be sent. This URL should be the URL of the page that the user is redirected to after successful authentication.

### Revocation Endpoint:

OAuth 2.0 doesn’t prescribe a specific format for access tokens, so you can use opaque tokens, JWT, or any other format that satisfies the necessary properties.
Revoking a refresh token via the revocation endpoint will not revoke the respective access token.
Revoking an access token via the revocation endpoint will not revoke the respective refresh token.

### UserInfo Endpoint:

Used to provide information about a user with an access token.
An access token can be used to invoke the userinfo endpoint to obtain user information as a payload. These claims in the payload are normally represented by a JSON object that contains a collection of name and value pairs for the claims. The format of the curl command is given below.

https://is.docs.wso2.com/en/6.1.0/guides/access-delegation/invoke-oauth-introspection-endpoint/
https://is.docs.wso2.com/en/latest/guides/authentication/oidc/revoke-tokens/

