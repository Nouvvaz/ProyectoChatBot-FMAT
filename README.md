# FMAT UADY Virtual Assistant

[![Status](https://img.shields.io/badge/Project%20Status-Phase%201%3A%20Requirements%20%26%20Design-orange.svg)]()
[![Documentation](https://img.shields.io/badge/Docs-Requirements%20Specification-blue.svg)](docs/requirements.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

An institutional conversational agent designed to centralize and automate student inquiries, administrative workflows, and academic procedures for the Faculty of Mathematics (FMAT) at the Autonomous University of Yucatan (UADY).

---

## Project Overview

Navigating university administrative services often involves fragmented information and peak consultation bottlenecks. This project delivers an automated virtual assistant powered by a local Retrieval-Augmented Generation (RAG) pipeline grounded in official FMAT documentation. 

The system aims to resolve routine student inquiries regarding academic calendars, enrollment, revalidation, and degree requirements, reducing the operational load on administrative offices.

---

## Current Status: Phase 1 (System Specification)

This repository currently contains the formal requirements specification and architectural definitions for the platform. No application source code has been committed yet.

- Detailed Functional and Non-Functional Requirements: [docs/requirements.md](docs/requirements.md)
- Next Deliverable: Architectural design, data model, and API contracts.

---

## Architectural Highlights

Based on the system requirements specification:
- **Local RAG & LLM Engine:** Processing of queries strictly bounded by institutional documents[cite: 1, 6].
- **Ephemeral Session Management:** In-memory, stateless student sessions with automatic expiration and no log persistence of PII[cite: 1, 2, 5].
- **Administrative Portal:** Secure document ingestion, intention management, and live vector re-indexing without service disruption[cite: 2, 3].
- **RESTful API Service:** Decoupled backend architecture exposing OpenAPI/Swagger specifications[cite: 3, 6].
- **High-Throughput Guardrails:** IP-based rate limiting, input sanitization, and fallback routing to faculty personnel[cite: 1, 2, 5].

## Repository Structure

```text
.
├── Docs/
│   ├── HistoriasDelUsuario/
│   ├── requirements/
│   │   ├── 01-Introduction.md
│   │   ├── 02-overall-description.md
│   │   ├── 03-Interface.md
│   │   ├── 04-Functional-Requirements.md
│   │   ├── 05-Non-Functional-Requirements.md
│   │   └── README.MD
│   ├── Use-Case-Specifications/
└── README.md