# Non-Functional Requirements (NFR)

Non-functional requirements specify the system quality attributes, operational thresholds, security standards, and architectural constraints governing the FMAT UADY Virtual Assistant.

---

## 1. Performance and Efficiency

This section defines system response benchmarks, concurrency goals, and compute resource protection mechanisms under variable academic loads.

| ID | Requirement | Specification / Acceptance Criteria | Priority |
| :--- | :--- | :--- | :--- |
| **NFR01** | Response Latency | The backend service must respond in $\le 12$ seconds for queries generated through the local RAG/LLM model, and $\le 5$ seconds for direct intent matches and static predefined responses[cite: 12]. | High[cite: 12] |
| **NFR02** | Concurrency & Throughput | The backend architecture must be optimized to process simultaneous incoming HTTP requests during high-demand calendar events (such as re-enrollment periods)[cite: 12]. | High[cite: 12] |
| **NFR03** | Request Rate Limiting | The backend must enforce IP-based rate limiting controls to protect local RAG compute capacity from resource exhaustion and Denial-of-Service (DoS) abuse[cite: 13]. | Medium[cite: 13] |

---

## 2. Security, Privacy, and Authentication

Guidelines safeguarding student privacy, encrypting data channels, and securing administrative interfaces against web threats.

| ID | Requirement | Specification / Acceptance Criteria | Priority |
| :--- | :--- | :--- | :--- |
| **NFR04** | Transport Security & Endpoint Protection | All network communication across the platform must enforce HTTPS encryption[cite: 13]. Administrative endpoints must be restricted via JSON Web Token (JWT) authorization[cite: 13]. | High[cite: 13] |
| **NFR05** | Sensitive Data Protection in Logs | The backend must neither capture nor persist personally identifiable information (PII) or sensitive user data (e.g., student IDs, legal names, or emails) within application logs[cite: 13]. | High[cite: 13] |
| **NFR06** | Input Sanitization & Threat Mitigation | The backend must validate and sanitize all raw incoming text payloads to prevent SQL Injection, Prompt Injection, and Cross-Site Scripting (XSS) attacks[cite: 13]. | High[cite: 13] |

---

## 3. Architecture, Software Quality, and Reliability

Directrices ensuring code maintainability, grounded generation reliability, and continuous system uptime.

| ID | Requirement | Specification / Acceptance Criteria | Priority |
| :--- | :--- | :--- | :--- |
| **NFR07** | OOP Design & SOLID Principles | The backend code must adhere to Object-Oriented Programming (OOP) paradigms and SOLID principles to maintain high cohesion and low coupling across service layers[cite: 13, 14]. | Medium[cite: 13] |
| **NFR08** | Interactive API Documentation | The backend must expose an interactive OpenAPI/Swagger specification to facilitate client integration and developer testing[cite: 14]. | High[cite: 14] |
| **NFR09** | Context Grounding & Fallback Strategy | Generative model responses must remain strictly bounded by context retrieved from official FMAT documentation, executing a deterministic fallback response when uncertainty is elevated or knowledge is absent[cite: 14]. | High[cite: 14] |
| **NFR10** | Service Availability (Uptime) | The backend service must maintain an operational availability target of at least 98% during active university service hours[cite: 14]. | High[cite: 14] |

---

## 4. Deployment, Maintainability, and Usability

Operational specifications addressing automated integration pipelines, containerized deployment, and multi-device presentation.

| ID | Requirement | Specification / Acceptance Criteria | Priority |
| :--- | :--- | :--- | :--- |
| **NFR11** | Continuous Integration (CI) | The GitHub repository must integrate automated GitHub Actions workflows to execute unit test suites across controllers and services prior to merging pull requests[cite: 14]. | Low[cite: 14] |
| **NFR12** | Containerization & Portability | The backend service and local LLM runtime must be containerized using Docker to ensure reproducibility across local workstations and faculty deployment infrastructure[cite: 14, 15]. | Medium[cite: 14] |
| **NFR13** | Response Usability | The assistant must deliver concise, structured answers (step-by-step workflows or bulleted lists) maintaining a clear, formal tone in Spanish[cite: 15]. | Medium[cite: 15] |
| **NFR14** | Responsive Layout | The client user interface must render adaptively across both desktop and mobile web browsers[cite: 15]. | High[cite: 15] |