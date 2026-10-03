# 1. Introduction

The **FMAT UADY Virtual Assistant** is an institutional conversational agent designed to centralize, streamline, and organize access to academic information, administrative workflows, and student services for the Faculty of Mathematics (FMAT) at the Autonomous University of Yucatan (UADY).

---

## 1.1 Purpose

The primary objective of this system is to deliver immediate, accurate, and automated guidance regarding institutional procedures, academic calendar deadlines, graduation requirements, and campus services. By integrating a context-grounded conversational agent, the platform reduces administrative workloads during peak inquiry periods and enhances student self-service efficiency.

The target audience comprises:
- Currently enrolled undergraduate and graduate students (predominantly aged 17–30 years).
- Prospective applicants seeking academic program offerings, admission guidelines, and faculty information.
- Faculty members and administrative personnel requiring quick references to institutional directories and regulations.

---

## 1.2 Scope

The product under development is an institutional conversational assistant, officially designated as the **FMAT UADY Virtual Assistant**. 

The system functions as a first-line digital support desk that interprets natural language inquiries and delivers deterministic, verified answers strictly grounded in official faculty documentation.

### Core Capabilities
- Resolving recurring inquiries regarding study plans, academic calendars, course re-enrollment, social service, and graduation protocols[cite: 1].
- Managing temporary, anonymous chat sessions with zero persistent logging of conversation histories or personal identifiable information[cite: 2, 5].
- Classifying user intents and routing unresolvable or low-certainty queries directly to official contacts at *Control Escolar* or *Secretaría Académica*[cite: 1, 2].
- Providing an authenticated administrative back-office to manage source documents, configure intents, and trigger dynamic vector re-indexing[cite: 2, 3].

### System Boundaries
The Phase 1 scope is strictly limited to information retrieval, advisory guidance, and administrative knowledge management. The platform does not perform direct write operations or record updates within the institutional student records platform (SICEI), nor does it process financial payments or tuition transactions.

---

## 1.3 Project Personnel

| Field | Detail |
| :--- | :--- |
| **Name** | Angel Eduardo Morales Ruiz |
| **Role** | Project Lead & Software Architect |
| **Professional Category** | Software Engineering Student |
| **Responsibilities** | Plans and coordinates project milestones, oversees requirements engineering, designs the system architecture, guides the local RAG pipeline specification, and manages repository governance. |
| **Contact Information** | `a25216432@alumnos.uady.mx` |
| **Approval** | Review and approval of architectural decisions, system requirements, and delivery milestones. |

| Field | Detail |
| :--- | :--- |
| **Name** | Melchor Emmanuel Ya Pérez |
| **Role** | UI/UX Designer & Frontend Engineer |
| **Professional Category** | Software Engineering Student |
| **Responsibilities** | Conducts user interface research, creates responsive design wireframes, defines client interaction patterns, and ensures adherence to accessibility standards for web clients[cite: 7]. |
| **Contact Information** | `a25216423@alumnos.uady.mx` |
| **Approval** | Review and validation of user interface mockups, design systems, and client usability. |

| Field | Detail |
| :--- | :--- |
| **Name** | Fernando Gael Ramos Barabato |
| **Role** | Backend Developer & QA Engineer |
| **Professional Category** | Software Engineering Student |
| **Responsibilities** | Develops core REST API endpoints, designs intent data structures, implements automated test suites, and configures continuous integration workflows[cite: 3, 6]. |
| **Contact Information** | *[Pending]* |
| **Approval** | Review and validation of service endpoints, data schemas, and test execution reports. |

---

## 1.4 Definitions, Acronyms, and Abbreviations

| Term / Acronym | Definition |
| :--- | :--- |
| **FMAT** | Facultad de Matemáticas (Faculty of Mathematics, UADY). |
| **UADY** | Universidad Autónoma de Yucatán (Autonomous University of Yucatan). |
| **SRS** | Software Requirements Specification. A formal technical document detailing system requirements, constraints, and operational behaviors. |
| **FR** | Functional Requirement. A specification defining an explicit function or behavior the system must perform[cite: 1]. |
| **NFR** | Non-Functional Requirement. A specification defining system performance, security, architecture, or quality attributes[cite: 4]. |
| **RAG** | Retrieval-Augmented Generation. An AI architecture that retrieves relevant document segments to ground model responses in verified facts[cite: 1, 6]. |
| **LLM** | Large Language Model. A neural network architecture used to interpret natural language queries and synthesize responses[cite: 1, 6]. |
| **SICEI** | Sistema de Control Escolar Institucional. UADY's central student records system. |
| **Ephemeral Session** | A transient session state stored exclusively in volatile memory, expiring after 30 minutes of inactivity or browser tab termination[cite: 1, 2]. |
| **Intent** | A semantic classification category mapped to specific user inquiries (e.g., `Consulta_Fecha_Reinscripcion`)[cite: 1]. |
| **Fallback** | A controlled default behavior triggered when model certainty is insufficient, redirecting users to human administrative contacts[cite: 1, 2]. |
| **PII** | Personally Identifiable Information (such as names, student enrollment IDs, and personal email addresses)[cite: 5]. |
| **JWT** | JSON Web Token. A compact, URL-safe standard used for cryptographically securing administrative API endpoints[cite: 5]. |
| **Rate Limiting** | An infrastructure control enforcing request quotas per IP address to safeguard services against resource exhaustion[cite: 5]. |
| **Vector Database** | A specialized database designed to store, index, and query vector embeddings generated from institutional documentation[cite: 3]. |
| **Interface** | The technical boundary across which users interact with the system or software components exchange payloads[cite: 3, 7]. |

---

## 1.5 References

| Reference | Title | Source / Path | Date | Author / Entity |
| :---: | :--- | :--- | :---: | :--- |
| **[Ref. 01]** | Requirements and System Guidelines Specification (Phase 1)[cite: 1] | Project Specification Assets[cite: 1] | 2026 | Project Development Team |
| **[Ref. 02]** | IEEE Std 830-1998 / ISO/IEC/IEEE 29148:2018 Standards | International Software Engineering Standards | 2018 | IEEE Computer Society |
| **[Ref. 03]** | Official Academic Regulations and Academic Calendar | FMAT UADY Institutional Portal | 2026 | Facultad de Matemáticas, UADY |

> *Note:* Specific operational manuals and institutional data handling policies will be added to this section as they are released by faculty authorities during upcoming development phases.

---

## 1.6 Document Overview

This document establishes the Software Requirements Specification for the FMAT UADY Virtual Assistant across the following sections.