# FMAT UADY Virtual Assistant

An institutional conversational agent designed to centralize and automate student inquiries, administrative workflows, and academic procedures for the Faculty of Mathematics (FMAT) at the Autonomous University of Yucatan (UADY).

---

## Deliverables & Course Milestones

| # | Deliverable | Due Date | Status | Resource / Link |
| :-: | :--- | :-: | :-: | :--- |
| 1 | Phase 1: Requirements Specification | 01/10/2026 | Completed | [Watch Phase 1 Video] https://canva.link/sq8vxoj7gi1wfud |

---

## Development Team

| Name | Role | Responsibilities | Email |
| :--- | :--- | :--- | :--- |
| **Angel Eduardo Morales Ruiz** | Project Lead & Software Architect | Project coordination, architecture design, RAG pipeline planning, requirements engineering, and repository governance. | `a25216432@alumnos.uady.mx` |
| **Melchor Emmanuel Ya Pérez** | UI/UX Designer & Frontend Engineer | User interface research, design system, responsive widget wireframes, client-side interactions, and accessibility compliance[cite: 15]. | `a25216423@alumnos.uady.mx` |
| **Fernando Gael Ramos Barabato** | Backend Developer & QA Engineer | RESTful API endpoint implementation, intent data schema definition, automated testing suites, and CI workflow management[cite: 11, 14]. | `a25216434@alumnos.uady.mx`|

---

## Project Overview

Navigating university administrative services often involves fragmented information and peak consultation bottlenecks during key calendar milestones. This project defines the technical foundation for an automated conversational assistant powered by a local Retrieval-Augmented Generation (RAG) architecture grounded in verified FMAT documentation[cite: 9, 14].

The platform aims to streamline student inquiries regarding study plans, academic calendars, re-enrollment periods, social service protocols, and graduation requirements, alleviating the repetitive administrative workload on faculty staff[cite: 9].

---

## Current Status: Phase 1 (System Specification)

This repository currently hosts the formal requirements specification and architectural baselines. Application source code and model configurations will be added in subsequent implementation phases.

- **System Requirements & Specifications:** Located in the [`docs/`](docs/) directory.
- **Next Deliverable:** Architectural system design, relational/vector data schema, and API contracts.

---

## Key System Specifications

- **Local Inference & RAG Pipeline:** Generates deterministic responses strictly bounded by official institutional documents to eliminate hallucinations[cite: 9, 14].
- **Ephemeral Session Management:** Volatile in-memory sessions that automatically expire after 30 minutes of inactivity or browser tab termination, maintaining zero PII in persistent logs[cite: 9, 10, 13].
- **Deterministic Intent Routing & Fallbacks:** Direct routing to official contacts at *Control Escolar* or *Secretaría Académica* when confidence scores fall below acceptable thresholds or queries fall out of scope[cite: 9, 10].
- **Administrative Portal:** Secure dashboard protected by JWT authentication to manage official documents, curate intents, and execute dynamic vector re-indexing without backend downtime[cite: 10, 11, 13].
- **RESTful API Architecture:** Decoupled backend service exposing structured JSON endpoints and interactive OpenAPI/Swagger documentation[cite: 11, 14].

---

## Repository Structure

```text
.
├── req/
│   ├── 01-introduction.md              # Project introduction, team roles, and scope
│   ├── 02-overall-description.md       # Product perspective, constraints, and assumptions
│   ├── 03-use-cases.md                 # System actors and formal use case specifications
│   ├── 05-Functional-Requirements.md   # Functional requirements catalog (FR01–FR16)
│   └── 06-Non-Functional-Requirements.md # Quality attributes, security, and performance
└── README.md                           # Main repository overview and milestone tracking
└── Video-Explanation.md