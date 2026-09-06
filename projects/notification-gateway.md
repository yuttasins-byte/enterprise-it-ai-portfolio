# Notification Gateway Platform

> A centralized API-based notification service designed to modernize legacy email delivery and provide controlled, auditable integration with Microsoft 365.

## Overview

Legacy applications often depend on direct SMTP configuration, shared credentials, and inconsistent delivery logging. The Notification Gateway Platform introduces a reusable service boundary between internal applications and the organization's email platform.

Applications call a controlled API rather than embedding mail-delivery logic and credentials independently.

## Architecture

```text
Internal Applications
        |
        | Authenticated REST API
        v
Notification Gateway
        |
        +----> Client Authorization
        +----> Sender Authorization
        +----> Request Validation
        +----> Delivery Logging
        |
        v
Microsoft Graph
        |
        v
Microsoft 365
```

## Key Design Areas

- centralized API-based email delivery
- Microsoft Graph integration
- application/service authentication
- allowed-sender controls
- delivery logging
- health and operational endpoints
- migration path from legacy SMTP

## Security Principles

- applications receive only the access they require
- sender identity is explicitly controlled
- credentials remain outside application source code
- requests and outcomes are auditable
- the gateway provides a single policy enforcement point

## Why a Gateway

A centralized notification layer reduces repeated integration work and creates a consistent migration path for applications that cannot immediately be redesigned.

It also separates business applications from changes in the underlying mail-delivery mechanism.

## Technology Stack

- Microsoft Graph
- FastAPI
- PostgreSQL
- Redis
- Docker
- REST APIs

## Business Value

- reduced dependency on legacy SMTP patterns
- reusable integration for multiple applications
- centralized authorization and logging
- simpler application onboarding
- improved traceability
- foundation for additional notification channels in the future

## Security & Confidentiality Note

This case study is intentionally sanitized. No production credentials, tenant identifiers, internal domains, email addresses, API tokens, or proprietary source code are published.

---

[Back to Portfolio](../README.md)
