# Internal AI Platform

> A secure enterprise AI assistant that connects organizational knowledge with structured internal systems while keeping identity, authorization, and system ownership explicit.

## Overview

The Internal AI Platform was designed to move beyond a standalone chatbot. Its purpose is to provide employees with a conversational interface for accessing organizational knowledge and approved operational data through controlled enterprise integrations.

The platform combines Retrieval-Augmented Generation (RAG) for knowledge-based questions with deterministic routing and Model Context Protocol (MCP) tools for structured business data.

## The Challenge

Enterprise users do not think in terms of APIs, databases, or application boundaries. They ask natural questions that may relate to knowledge documents, people, projects, venues, software, parking, catering, or other internal services.

This creates several engineering challenges:

- Route questions to the correct business domain without leaking context across domains.
- Separate knowledge retrieval from authoritative structured-data queries.
- Resolve natural-language references to canonical enterprise entities.
- Prevent AI-generated answers from inventing operational facts.
- Integrate systems without giving the AI direct database access across application boundaries.
- Maintain security, observability, testability, and predictable fallback behavior.

## Architecture

```text
User
  |
  v
Chat Interface
  |
  v
Intent / Domain Routing
  |
  +----------------------+----------------------+
  |                                             |
  v                                             v
Knowledge Path                              Structured Data Path
  |                                             |
  v                                             v
RAG / Examples                              MCP Tools
  |                                             |
  v                                             v
Knowledge Base                         Internal Service APIs
                                                |
                                                v
                                      Authoritative Systems
```

A simplified structured-data flow:

```text
Natural-language question
        |
        v
Domain ownership / intent
        |
        v
MCP tool
        |
        v
Internal API owned by source system
        |
        v
Canonical structured result
        |
        v
Deterministic response formatter
```

## Key Design Decisions

### 1. RAG and Structured Data Are Different Paths

Knowledge questions are answered from approved knowledge content through RAG. Operational facts such as project progress or workload are retrieved through structured APIs and MCP tools.

This prevents dynamic business data from being treated as static document knowledge.

### 2. Deterministic Domain Ownership

Domain-specific handlers identify whether a question belongs to a supported structured-data capability. Strong native-domain evidence is preferred over weak generic keywords.

When a question could reasonably refer to multiple domains, the long-term design favors explicit clarification rather than guessing.

### 3. MCP as the Integration Boundary

MCP tools provide a controlled interface between the assistant and enterprise services. The AI application does not need direct access to every source database.

This supports:

- service ownership boundaries
- reusable integrations
- controlled authentication
- structured payloads
- easier testing and auditing

### 4. Canonical Person Resolution

Natural references such as a person's name or nickname are resolved through an internal identity-resolution API owned by the source platform.

```text
User reference
   -> MCP resolve_user
   -> Internal user-resolution API
   -> canonical user_id
   -> authorized analytics query
```

The resolver can return `resolved`, `no_match`, or `ambiguous`. IDs are never invented when resolution is uncertain.

### 5. Grounded Operational Responses

Structured results are formatted deterministically rather than passed through an LLM solely for rewriting. This keeps operational numbers grounded while still presenting them in readable language.

### 6. Security by Design

Server-to-server integrations use dedicated service tokens and explicit internal API contracts. Sensitive configuration is kept outside source control.

Design principles include:

- least privilege
- fail-closed authentication
- explicit service boundaries
- no cross-system direct database dependency where an owned API is appropriate
- sanitized logging
- no credentials or secrets in prompts or repositories

## Capabilities

The platform architecture supports multiple enterprise domains, including:

- organizational knowledge retrieval
- employee/person resolution
- project progress and analytics
- workload and performance evidence
- venue information
- parking information
- software inventory
- catering information
- future workflow and service integrations

The architecture is intentionally extensible so additional domains can be introduced without turning the assistant into a single monolithic integration layer.

## Reliability and Observability

The platform includes operational controls such as:

- health checks
- structured runtime traces
- routing diagnostics
- MCP call outcome tracing
- cache versioning
- deterministic fallbacks
- sync/stream behavior regression tests
- containerized deployment

A shadow planning layer can evaluate routing decisions without controlling production behavior, allowing future routing approaches to be measured safely before promotion.

## Engineering Approach

The project follows several principles:

**Build Where It Creates Value**  
Build internal capabilities when they provide meaningful operational or strategic value, while integrating established platforms where appropriate.

**API First**  
Prefer owned, reusable service contracts over direct cross-application database coupling.

**AI Where Useful, Determinism Where Required**  
Use AI for language understanding and knowledge interaction, but retain deterministic controls for identity, authorization, routing boundaries, and operational facts.

**Human-Centered Interaction**  
When intent is ambiguous, guide the user toward the correct domain instead of silently making a risky assumption.

## Technology Stack

- Python
- FastAPI
- PostgreSQL
- Redis
- Docker
- REST APIs
- Model Context Protocol (MCP)
- Retrieval-Augmented Generation (RAG)
- OIDC / identity integration
- Structured logging and runtime tracing

## Business Value

The platform demonstrates how enterprise AI can become an integration and productivity layer rather than a disconnected chatbot.

Potential organizational value includes:

- faster access to internal knowledge
- simplified access to multiple business systems
- reduced navigation between applications
- reusable API and MCP integrations
- consistent identity and authorization boundaries
- a foundation for future workflow automation and AI-assisted operations

## Current Evolution

The platform continues to evolve in several areas:

- cross-domain clarification and routing
- knowledge chunk review and governance
- natural response quality
- multilingual interaction
- additional workflow integrations
- expanded observability and evaluation

## Security & Confidentiality Note

This case study is intentionally sanitized. Architecture and engineering patterns are presented at a portfolio level only. No production credentials, internal hostnames, IP addresses, employee records, confidential business data, or proprietary source code are published.

---

[Back to Portfolio](../README.md)
