# Identity & SSO Platform

> A centralized identity layer for internal applications using modern OAuth 2.0 and OpenID Connect patterns.

## Overview

The Identity & SSO Platform provides a reusable authentication foundation for internal applications. The objective is to reduce application-specific authentication logic and move toward consistent identity, token validation, and audit patterns.

## Architecture

```text
User
  |
  v
Internal Application
  |
  | Authorization Code + PKCE
  v
Identity Platform
  |
  +----> Authentication
  +----> Authorization Code
  +----> Token Issuance (RS256)
  +----> JWKS
  |
  v
Application Session / Authorized APIs
```

## Key Design Areas

- OAuth 2.0 Authorization Code Flow
- Proof Key for Code Exchange (PKCE)
- OpenID Connect
- RS256 asymmetric token signing
- JWKS-based public key distribution
- application/client registration
- redirect URI control
- standardized identity claims
- audit events

## Why Asymmetric Signing

Using RS256 allows applications to validate tokens with a public key without sharing the identity platform's signing secret.

```text
Identity Platform
   |
   | signs with private key
   v
JWT
   |
   | validated with public key / JWKS
   v
Internal Application
```

This creates a cleaner trust boundary than distributing a shared HMAC secret to multiple applications.

## Security Principles

- centralized authentication
- least privilege
- controlled client registration
- explicit redirect URIs
- short-lived authorization artifacts
- asymmetric signing
- auditable authentication events
- secrets kept outside source control

## Technology Stack

- OAuth 2.0
- OpenID Connect
- JWT
- RS256
- JWKS
- FastAPI
- PostgreSQL
- Docker

## Business Value

A shared identity layer can reduce duplicated authentication implementation, improve consistency across internal applications, and provide a foundation for stronger access governance as the internal application ecosystem grows.

## Security & Confidentiality Note

This case study describes sanitized architecture patterns only. No production keys, client secrets, internal domains, user records, or proprietary source code are published.

---

[Back to Portfolio](../README.md)
