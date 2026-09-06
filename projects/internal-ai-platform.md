# Sally Internal AI

> A secure internal AI assistant that connects organizational knowledge with approved structured systems while keeping identity, authorization, source ownership, and operational facts explicit.

## Overview

Sally Internal AI was designed to move beyond a standalone chatbot. Its purpose is to provide employees with a natural-language interface for accessing organizational knowledge and approved operational data through controlled integrations.

The platform combines Retrieval-Augmented Generation (RAG) for knowledge-based questions with deterministic domain routing and Model Context Protocol (MCP) tools for structured operational data.

The design goal is not to let an AI model freely query enterprise systems. Instead, Sally acts as a controlled interaction layer over existing APIs, identity boundaries, and authoritative source systems.

## The Challenge

Employees do not think in terms of APIs, databases, or application boundaries. They ask natural questions that may relate to knowledge documents, people, projects, venues, software, parking, catering, workflows, or other internal services.

This creates several engineering challenges:

- Route questions to the correct business domain without leaking context across domains.
- Separate knowledge retrieval from authoritative structured-data queries.
- Resolve natural-language references to canonical internal entities.
- Prevent AI-generated answers from inventing operational facts.
- Integrate systems without giving the AI unrestricted direct database access.
- Preserve application ownership and authorization boundaries.
- Maintain security, observability, testability, and predictable fallback behavior.
- Improve conversational quality without sacrificing deterministic controls.

## Architecture

```text
User
  |
  v
Chat Interface
  |
  v
Identity / Conversation Context
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
Approved Knowledge                    Internal Service APIs
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

### 1. RAG and Structured Data Use Different Paths

Knowledge questions are answered from approved knowledge content through RAG. Operational facts such as project progress, workload, inventory, or service information are retrieved through structured APIs and MCP tools.

This prevents dynamic business data from being treated as static document knowledge and reduces the risk of generated operational facts.

### 2. Deterministic Domain Ownership

Domain-specific handlers determine whether a question belongs to a supported structured-data capability. Strong native-domain evidence is preferred over weak generic keywords.

When a question could reasonably refer to multiple domains, the design favors clarification and bounded context rather than silently guessing.

### 3. MCP as a Controlled Integration Boundary

MCP tools provide a structured interface between Sally and internal services. The AI application does not need direct access to every source database.

This supports:

- clear service ownership boundaries
- reusable integrations
- controlled authentication
- structured request and response payloads
- easier testing and auditing
- safer expansion into additional domains

### 4. Canonical Person and Entity Resolution

Natural references such as a person's name or nickname are resolved through an internal identity-resolution capability owned by the source platform.

```text
User reference
   -> MCP resolve_user
   -> Internal resolution API
   -> canonical user_id
   -> authorized operational query
```

The resolver can return `resolved`, `no_match`, or `ambiguous`. IDs are never invented when resolution is uncertain.

### 5. Grounded Operational Responses

Structured results are formatted deterministically rather than relying on an LLM to invent or reinterpret operational values. AI is used where language flexibility adds value; deterministic logic remains in control where correctness matters.

### 6. Identity-Aware, Secure-by-Design Integration

Authentication and authorization are explicit parts of the architecture. Server-to-server integrations use dedicated service credentials and defined internal API contracts, while sensitive configuration remains outside source control.

Design principles include:

- least privilege
- fail-closed authentication
- explicit service boundaries
- identity-aware access
- no unnecessary cross-system direct database dependency
- sanitized logging
- no credentials or secrets in prompts or repositories

## Current Capabilities

The platform architecture supports multiple internal domains, including:

- organizational knowledge retrieval
- employee/person resolution
- project progress and analytics
- workload and performance evidence
- venue information
- parking information
- software inventory
- catering information
- conversation context and bounded follow-up handling
- extensible workflow and service integrations

The architecture is intentionally modular so additional domains can be introduced without turning the assistant into a monolithic integration layer.

## Reliability, Testing & Observability

Operational controls include:

- health checks
- structured runtime traces
- routing diagnostics
- MCP call outcome tracing
- cache versioning
- deterministic fallbacks
- regression testing for structured handlers
- sync/stream behavior validation
- containerized deployment

A shadow planning layer can evaluate alternative routing decisions without controlling production behavior. This allows future approaches to be measured safely before promotion.

## Engineering Approach

**Build Where It Creates Value**  
Build internal capabilities when they provide meaningful operational or strategic value, while integrating established platforms where appropriate.

**API First**  
Prefer owned, reusable service contracts over direct cross-application database coupling.

**AI Where Useful, Determinism Where Required**  
Use AI for language understanding, knowledge interaction, and conversational flexibility while retaining deterministic controls for identity, authorization, routing boundaries, and operational facts.

**Human-Centered Interaction**  
When intent is ambiguous, guide the user toward the correct domain instead of silently making a risky assumption.

**Observable Before Autonomous**  
New AI-assisted routing or planning behavior should be measurable and traceable before it is allowed to control production outcomes.

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

Sally demonstrates how internal AI can become a secure interaction and integration layer rather than a disconnected chatbot.

Potential organizational value includes:

- faster access to approved internal knowledge
- simpler access to information distributed across multiple systems
- reduced navigation between applications
- reusable API and MCP integrations
- consistent identity and authorization boundaries
- grounded answers for operational data
- a foundation for workflow automation and AI-assisted operations

## Current Evolution

The platform continues to evolve in several areas:

- natural conversation and contextual follow-up
- cross-domain clarification and routing
- knowledge review and governance
- multilingual interaction
- workflow and ticket integrations
- evaluation and observability
- controlled use of additional AI models where they provide measurable value

## Security & Confidentiality Note

This case study is intentionally sanitized. Architecture and engineering patterns are presented at a portfolio level only. No production credentials, internal hostnames, IP addresses, employee records, confidential business data, or proprietary source code are published.

---

[Back to Portfolio](../README.md)
