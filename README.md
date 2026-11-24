# Yuttasin Srisangchan — Enterprise IT Infrastructure, Cybersecurity & AI Systems Portfolio

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin)](https://www.linkedin.com/in/yuttasin-srisangjan-343767290/)
[![Award](https://img.shields.io/badge/Award-R2I%202026%20Best%20Innovation-gold?style=flat)](#awards--recognition)
[![Focus](https://img.shields.io/badge/Focus-IT%20Infrastructure%20%7C%20Cybersecurity%20%7C%20Self--Hosted%20AI-1E293B?style=flat)](#core-competencies)

**IT Infrastructure & Cyber Security Leader** with **17+ years of enterprise experience** across healthcare, financial lending, retail, and large-scale exhibition venues. Proven track record in designing resilient multi-branch networks, hardening hybrid server & container environments, driving cost-effective open-source modernization, and architecting secure on-premises enterprise AI ecosystems.

---

## Executive Highlights & Business Impact

* **Enterprise Digital Transformation (R2I 2026 Winner):** Architected and delivered an all-in-one **Internal IT Services Web Portal** unifying asset/license lifecycle management, paperless approvals, project tracking, and live infrastructure monitoring—winning **The Best System & Process Innovation Award (R2I 2026)**.
* **On-Premises Enterprise AI Architecture:** Designed a private, self-hosted **Enterprise Internal AI Chatbot** (`Ollama` + `RAG` + `MCP Gateway`) integrated with **Active Directory (OIDC)** and **Microsoft Graph**, enabling secure internal knowledge retrieval without exposing corporate data to public cloud LLMs.
* **DevSecOps & Container Hardening:** Implemented automated **Trivy** container vulnerability scanning (pre- & post-production) and modernized legacy PHP applications onto hardened container base images, reducing critical CVEs from **28 to 0**.
* **Strategic Cost Optimization:**
  * Restructured enterprise telephony by migrating to an on-premises **3CX** architecture, reducing 3-year maintenance costs by **~70%** (~300K THB vs. 1M THB legacy MA).
  * Consolidated endpoint security across **800+ endpoints**, lowering per-license cost by **~27%** while strengthening threat visibility.
  * Streamlined network maintenance (MA) contracts by bringing backup and configuration management in-house.
* **Hyper-Scale Branch Rollout:** Planned, designed, and deployed standardized enterprise network infrastructure supporting rapid expansion from **2,000 to 6,000 branches within 12 months**.

---

## Featured Enterprise Architectures & Case Studies

### 1. Self-Hosted Enterprise AI & MCP Ecosystem
A privacy-first internal AI platform built to serve corporate users while enforcing strict identity governance and zero external data leakage.

```mermaid
flowchart LR
    User([Enterprise Users]) -->|SSO / OIDC| WebUI[Internal AI Web Portal]
    WebUI --> Auth[Active Directory OIDC]
    WebUI --> Gateway[MCP Gateway & Orchestrator]
    Gateway --> LLM[Self-Hosted Ollama LLM]
    Gateway --> RAG[(Enterprise RAG Vector DB)]
    Gateway --> Graph[Microsoft Graph Notifications]
    Gateway --> ITSM[IT Services & Monitoring APIs]
