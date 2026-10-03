# 2. Overall Description

This section establishes the high-level technical perspective, architectural boundaries, user roles, operating constraints, and foundational assumptions governing the FMAT UADY Virtual Assistant.

---

## 2.1 Product Perspective

The FMAT UADY Virtual Assistant is a standalone, web-accessible conversational system engineered to interface directly with the institutional web ecosystem of the Faculty of Mathematics (FMAT - UADY). It operates as a decoupled client-server platform optimized for local execution and strict data privacy.

### System Interfaces and Decomposition

- **User Client Interface:** A lightweight, embeddable web component designed to adapt responsively to mobile and desktop browsers[cite: 7].
- **RESTful API Service:** The backend exposes stateless REST endpoints (e.g., `POST /api/v1/chat/message`) consuming and delivering structured JSON payloads[cite: 3].
- **Interactive Documentation Interface:** Exposes an interactive OpenAPI/Swagger specification for simplified frontend consumption and testing[cite: 6].
- **Knowledge Base & Vector Store:** Specialized high-dimensional vector store supporting dynamic re-indexing without backend downtime[cite: 3].
- **Local Inference Engine:** Executes local Large Language Model (LLM) inference strictly bounded by official FMAT context documents[cite: 1, 6].

---

## 2.2 Product Functions

The core functionalities of the system are decomposed into the following operational capabilities:

- **Context-Grounded Query Resolution:** Interprets natural language questions regarding administrative procedures (re-enrollment, transcripts, degree requirements, social service, scholarships, and academic calendars) utilizing a local RAG engine grounded in verified institutional documents[cite: 1].
- **Intent Classification & Fast Retrieval:** Classifies incoming user queries into discrete operational intents (e.g., `Consulta_Fecha_Reinscripcion`, `UbicacionLaboratorio`, `Requisitos_Titulacion`) to accelerate response times and retrieve deterministic static answers[cite: 1].
- **Automated Fallback & Channeling:** Triggers predefined fallback messages redirecting users to official contacts at *Control Escolar* or *Secretaría Académica* when retrieval confidence falls below configured thresholds or information is unavailable[cite: 1, 2].
- **Domain Boundary Enforcement:** Detects and filters out queries unrelated to academic offerings, student workflows, or faculty operations[cite: 2].
- **External Dependency Routing:** Provides general orientation and contact details for procedures governed by outside institutional dependencies (e.g., IMSS healthcare registration, CIL English language courses, and external scholarships).
- **Ephemeral Session Management:** Instantiates non-persistent, anonymous chat sessions in volatile memory, recording messages chronologically and wiping all transient history after 30 minutes of inactivity or browser tab closure[cite: 1, 2].
- **Knowledge Base Administration:** Authenticates administrators via credentials to manage documents, perform intent CRUD operations, and trigger dynamic vector re-indexing without system restarts[cite: 2, 3].
- **Structured Response Delivery:** Delivers responses parsed with Markdown formatting, rendering bold text, lists, and direct links to official forms and institutional regulations[cite: 3].

---

## 2.3 User Classes and Characteristics

The system defines two primary user classes with distinct interaction profiles:

| User Class | Profile & Interaction Mode | Technical Expertise | System Privileges |
| :--- | :--- | :--- | :--- |
| **Student / General Visitor** | Anonymous end users interacting via desktop or mobile web browsers to resolve academic questions[cite: 2, 7]. Expects concise, step-by-step guidance in formal Spanish[cite: 7]. | Low to Intermediate | Unauthenticated, read-only interaction with conversational endpoints via ephemeral sessions[cite: 2, 3]. |
| **System Administrator** | Faculty administrative personnel or IT staff responsible for curating official documents and managing intent catalogs[cite: 3]. | Intermediate to Advanced | Authenticated via username and password, authorized through JSON Web Tokens (JWT) to access management endpoints[cite: 2, 3, 5]. |

---

## 2.4 Design and Operational Constraints

### 1. Performance and Efficiency Constraints
- **Latency Upper Bounds:** Response latency must not exceed 12 seconds for local RAG/LLM inferences, and must remain within 5 seconds for direct static intents[cite: 4].
- **Concurrency Optimization:** Backend throughput must be architected to handle concurrent HTTP requests during peak academic calendar events (such as re-enrollment windows)[cite: 4].
- **Network Abuse Prevention:** IP-based rate limiting controls must be enforced to protect the local RAG engine from resource exhaustion and Denial-of-Service (DoS) events.

### 2. Security and Data Privacy Constraints
- **Transport Security:** All communications between clients, APIs, and administrative modules must be encrypted via HTTPS[cite: 5].
- **Endpoint Authorization:** Administrative routes must be strictly guarded via JWT validation[cite: 5].
- **Zero PII Logging:** Backend services are strictly prohibited from storing personally identifiable information (e.g., student IDs, legal names, email addresses) within log files[cite: 5].
- **Input Sanitization:** The backend must sanitize all incoming query payloads to prevent SQL Injection, Prompt Injection, and Cross-Site Scripting (XSS) exploits[cite: 5].

### 3. Software Architecture and Maintainability Constraints
- **OOP & SOLID Principles:** The codebase must follow Object-Oriented Programming principles with high cohesion and low coupling across service layers[cite: 5, 6].
- **Continuous Integration:** The repository must incorporate automated GitHub Actions workflows executing unit test suites prior to code merging[cite: 6].
- **Containerized Portability:** Both the backend application and local LLM runtime must be fully containerized using Docker to ensure deployment reproducibility.
- **Service Reliability:** The system must maintain an operational availability target of at least 98% during university operating hours[cite: 6].

---

## 2.5 Assumptions and Dependencies

### Assumptions
- **Institutional Documentation Integrity:** Official documentation, academic calendars, curriculum structures, and procedure guides provided by FMAT are authoritative, current, and unambiguous[cite: 1, 4].
- **Client Web Standards:** End users access the chat interface using modern web browsers supporting ECMAScript 6+ and standard DOM manipulation[cite: 7].
- **Stateless Anonymous Use:** Students do not require persistent conversation history across sessions or devices, accepting automatic 30-minute memory purges[cite: 1, 2].

### Dependencies
- **Host Infrastructure:** Local physical or virtual host machines must provide adequate computational resources (CPU/RAM/GPU) to sustain containerized local model inference within latency thresholds[cite: 4, 6, 7].
- **Institutional Network Connectivity:** The host environment depends on stable institutional intranet and internet routing to serve client requests securely via HTTPS[cite: 5].

---

## 2.6 Apportioning of Requirements & Future Enhancements

The following capabilities are formally deferred to future development phases and are out of scope for Phase 1:

- **SICEI Database Integration:** Direct integration with the institutional academic database to enable authenticated queries regarding personal grades and active student status.
- **Multilingual Support:** Inclusion of regional indigenous language support (Yucatec Maya) and internationalization in English.
- **Auditory Interaction:** Integration of Speech-to-Text (STT) and Text-to-Speech (TTS) pipelines for visually impaired accessibility.
- **Automated Web Scraping:** Scheduled crawlers to automatically index news bulletins and urgent announcements published on the official FMAT portal.