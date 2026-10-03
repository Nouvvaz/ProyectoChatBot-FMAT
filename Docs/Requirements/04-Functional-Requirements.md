# Functional Requirements (FR)

Functional requirements define the core operational behaviors, conversational workflows, administrative tools, and interaction endpoints governing the FMAT UADY Virtual Assistant.

---

## 1. User Inactivity and Ephemeral Session Management

This section specifies session lifecycle rules, volatile conversational state retention, and automatic data clearance mechanisms ensuring user privacy.

| ID | Requirement | Description / Behavioral Specification | Priority |
| :--- | :--- | :--- | :--- |
| **FR01** | Session Expiration & Auto-Cleanup | The system must automatically terminate the chat session and purge all transient conversation history after 30 minutes of user inactivity or immediately upon closing the browser tab/window[cite: 9]. | High[cite: 9] |
| **FR06** | Anonymous Session Instantiation | The system must instantiate a transient, in-memory session object (non-persisted in persistent storage) to maintain dialogue context while the user interacts with the interface[cite: 10]. | High[cite: 10] |
| **FR07** | Ephemeral Message Logging | The backend must record each incoming user query and generated response sequentially within temporary session memory strictly for the active duration of the session[cite: 10]. | High[cite: 10] |
| **FR08** | Privacy Notice Display | The client user interface must visibly display a privacy banner informing users that conversations are anonymous and no history is retained once the session terminates[cite: 10]. | Medium[cite: 10] |

---

## 2. RAG Engine, Query Processing, and Domain Guardrails

Specifications governing natural language understanding, institutional knowledge retrieval, scope delimitation, and graceful fallback routing.

| ID | Requirement | Description / Behavioral Specification | Priority |
| :--- | :--- | :--- | :--- |
| **FR02** | Academic Query Processing (RAG) | The conversational engine must interpret natural language inquiries regarding academic procedures (re-enrollment, transcripts, degree certification, social service, scholarships, and academic calendars) utilizing a local RAG/LLM architecture grounded in official FMAT documentation[cite: 9]. | High[cite: 9] |
| **FR03** | Intent Categorization & Dispatch | The system must classify incoming user input into predefined semantic intents (e.g., `Consulta_Fecha_Reinscripcion`, `UbicacionLaboratorio`, `Requisitos_Titulacion`) to optimize retrieval and deliver static or semantic responses efficiently[cite: 9]. | High[cite: 9] |
| **FR04** | Direct Channeling & Informational Fallback | When retrieval confidence falls below the configured minimum threshold or required data is missing from the knowledge base, the system must trigger a predefined fallback response and provide direct contact details for *Control Escolar* or *Secretaría Académica*[cite: 9, 10]. | High[cite: 9] |
| **FR05** | Domain Boundary Filtering | The backend must analyze incoming prompts to detect and reject out-of-scope inquiries unrelated to FMAT educational programs, student procedures, or campus activities[cite: 10]. | High[cite: 10] |

---

## 3. System Administration and Knowledge Base Management

Capabilities provided to authorized faculty staff to manage institutional source materials, configure intent mappings, and re-index vector collections dynamically.

| ID | Requirement | Description / Behavioral Specification | Priority |
| :--- | :--- | :--- | :--- |
| **FR09** | Administrator Authentication | The system must authenticate administrative users via username and password credentials prior to granting access to the administrative control panel[cite: 10, 11]. | High[cite: 10] |
| **FR10** | Document Ingestion & Catalog Management | The administrative module must allow authorized operators to upload, update, and manage official regulatory documents and files feeding the retrieval knowledge base[cite: 11]. | Medium[cite: 11] |
| **FR11** | Intent CRUD Lifecycle Management | Administrators must be able to create, read, update, and delete intents, associated keywords, and direct deterministic static responses[cite: 11]. | Medium[cite: 11] |
| **FR12** | Dynamic Vector Re-indexing | The system must dynamically update and re-index the vector knowledge base upon adding, updating, or deleting official documents without requiring backend server restarts[cite: 11]. | High[cite: 11] |

---

## 4. Integration Interfaces and Institutional Guidance Services

Endpoints, response markup formatting, and procedural routing connecting the backend service to the user presentation layer.

| ID | Requirement | Description / Behavioral Specification | Priority |
| :--- | :--- | :--- | :--- |
| **FR13** | Message Ingestion REST Endpoint | The backend must expose a dedicated REST endpoint (e.g., `POST /api/v1/chat/message`) accepting incoming user queries in JSON format and returning structured JSON payload responses[cite: 11]. | High[cite: 11] |
| **FR14** | Markdown Parsing & Direct Hyperlinks | The backend must return responses formatted in Markdown to support bold typography, ordered/unordered lists, and direct functional hyperlinks to institutional forms and regulatory documents[cite: 11]. | Medium[cite: 11] |
| **FR15** | Procedural Workflow Guidance | The system must deliver structured, sequential steps, prerequisite checklists, and validity timelines for official school paperwork (e.g., transcript issuance) based on current FMAT guidelines[cite: 12]. | Medium[cite: 12] |
| **FR16** | External Dependency Channeling | The system must offer general guidance and provide official external contacts when inquiries involve procedures beyond the direct jurisdiction of *Control Escolar* (e.g., IMSS healthcare coverage, CIL language certifications, external scholarships, or student ID credentials)[cite: 12]. | Medium[cite: 12] |