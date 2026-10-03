# User Stories (Agile Specifications)

This document contains the user stories for the FMAT UADY Virtual Assistant project. Each story follows the standard Agile format (*Role - Goal - Benefit*) and includes acceptance criteria mapped to our functional and non-functional requirements[cite: 9, 10, 11, 12, 13].

---

## Summary Table

| ID | Story Title | User Role | Priority | Mapped Requirements |
| :---: | :--- | :--- | :---: | :--- |
| **US01** | Anonymous Chat Session & Privacy Notice | Student / Visitor | High | RF06, RF08[cite: 10] |
| **US02** | Automatic Inactivity Session Expiration | Student / Visitor | High | RF01, RF07, RNF05[cite: 9, 10, 13] |
| **US03** | Academic Inquiries via Local RAG | Student / Visitor | High | RF02, RF15, RNF01, RNF09[cite: 9, 12, 14] |
| **US04** | Fast Predefined Intent Resolution | Student / Visitor | High | RF03, RNF01[cite: 9, 12] |
| **US05** | Fallback and Low-Certainty Channeling | Student / Visitor | High | RF04, RF05, RNF09[cite: 9, 10, 14] |
| **US06** | External Dependency Guidance | Student / Visitor | Medium | RF16, FR14[cite: 11, 12] |
| **US07** | Markdown Formatting & Official Links | Student / Visitor | Medium | RF14, RNF13[cite: 11, 15] |
| **US08** | Administrator Login via JWT | Administrator | High | RF09, RNF04[cite: 10, 11, 13] |
| **US09** | Official Document Ingestion | Administrator | Medium | RF10, RNF04[cite: 11, 13] |
| **US10** | Live Vector Re-indexing | Administrator | High | RF12, RNF04[cite: 11, 13] |
| **US11** | Intent & Static Answer Management (CRUD) | Administrator | Medium | RF11[cite: 11] |
| **US12** | Mobile & Desktop Responsive Interaction | Student / Visitor | High | RNF14[cite: 15] |

---

## Epic 1: Session Management & Privacy

### US01: Anonymous Chat Session & Privacy Notice
* **As a** student or visitor,
* **I want to** start a conversation immediately without logging in and see a clear privacy statement,
* **So that** I know my personal data is protected and my identity remains anonymous[cite: 10].

#### Acceptance Criteria
1. When opening the chat widget, the system instantiates an ephemeral session in memory without asking for credentials or student ID[cite: 10].
2. A visible privacy banner displays a clear note explaining that conversations are anonymous and will not be retained after closing[cite: 10].
3. The chat displays an initial welcome message prompting the user for their query[cite: 10].
* **Traceability:** RF06, RF08[cite: 10].

---

### US02: Automatic Inactivity Session Expiration
* **As a** student,
* **I want** the system to automatically delete my temporary conversation history after a period of inactivity,
* **So that** subsequent users on shared campus computers cannot read my previous questions[cite: 9, 10].

#### Acceptance Criteria
1. The backend automatically terminates the chat session and wipes the in-memory message history after 30 minutes of inactivity[cite: 9, 10].
2. If the user closes the browser tab or window, the session terminates[cite: 9].
3. System logs do not store or persist any sensitive information, names, or student IDs typed during the session[cite: 13].
* **Traceability:** RF01, RF07, RNF05[cite: 9, 10, 13].

---

## Epic 2: Academic Inquiries & RAG Core

### US03: Academic Inquiries via Local RAG
* **As a** student,
* **I want to** ask questions in natural language about school procedures (re-enrollment, transcripts, degree requirements, social service, and calendars),
* **So that** I receive accurate, step-by-step guidance based on official FMAT regulations[cite: 9, 12].

#### Acceptance Criteria
1. The system interprets natural language queries in Spanish regarding FMAT academic topics[cite: 9, 15].
2. Answers are generated using a local RAG model strictly grounded in indexed institutional documents[cite: 9, 14].
3. The response time for RAG-generated answers must not exceed 12 seconds[cite: 12].
4. The output must clearly detail requirements, prerequisites, and official deadlines where applicable[cite: 12].
* **Traceability:** RF02, RF15, RNF01, RNF09[cite: 9, 12, 14].

---

### US04: Fast Predefined Intent Resolution
* **As a** student,
* **I want to** get direct answers to frequent questions (such as laboratory locations or office hours),
* **So that** I do not have to wait for heavy model inference times[cite: 9, 12].

#### Acceptance Criteria
1. The system detects specific intents (e.g., `UbicacionLaboratorio`, `Consulta_Fecha_Reinscripcion`)[cite: 9].
2. Predefined static answers are returned in $\le 5$ seconds[cite: 12].
3. The response matches the curated information set by administrators[cite: 9, 11].
* **Traceability:** RF03, RNF01[cite: 9, 12].

---

### US05: Fallback and Low-Certainty Channeling
* **As a** student,
* **I want** the assistant to redirect me to administrative offices when it does not know an answer or if my question is outside FMAT scope,
* **So that** I avoid false information (hallucinations) and get the official contact directly[cite: 9, 10, 14].

#### Acceptance Criteria
1. When semantic similarity is below the minimum threshold or the topic does not exist in the files, the bot triggers a fallback message[cite: 9, 14].
2. The bot provides direct contact information (emails/offices) for *Control Escolar* or *Secretaría Académica*[cite: 9, 10].
3. Questions unrelated to FMAT academic life are detected and politely rejected[cite: 10].
* **Traceability:** RF04, RF05, RNF09[cite: 9, 10, 14].

---

### US06: External Dependency Guidance
* **As a** student,
* **I want** guidance when asking about university services not handled by Control Escolar (IMSS health insurance, CIL language courses, external scholarships, or student credentials),
* **So that** I know which external dependency to visit and how to proceed[cite: 12].

#### Acceptance Criteria
1. The system identifies inquiries regarding non-FMAT university procedures[cite: 12].
2. The assistant provides an overview of the steps required and provides direct official contact details or links for the relevant dependency[cite: 11, 12].
* **Traceability:** RF16, RF14[cite: 11, 12].

---

## Epic 3: User Interface & Communication

### US07: Markdown Formatting & Official Links
* **As a** student,
* **I want to** view responses with organized formatting (bold text, lists, and clickable links),
* **So that** I can easily read long procedures and access official registration forms with a single click[cite: 11, 12, 15].

#### Acceptance Criteria
1. The backend delivers parsed text supporting Markdown markup[cite: 11].
2. The client renders lists, bold key terms, and valid hyperlinks directing to official faculty documents and forms[cite: 11].
3. The text is displayed in a formal, concise, and structured tone in Spanish[cite: 15].
* **Traceability:** RF13, RF14, RNF13[cite: 11, 15].

---

### US08: Mobile & Desktop Responsive Interaction
* **As a** student on campus,
* **I want to** access the chatbot from my smartphone or laptop without broken layouts,
* **So that** I can consult requirements while walking around campus or during class[cite: 15].

#### Acceptance Criteria
1. The web widget adapts fluidly to mobile viewports and desktop resolutions[cite: 15].
2. Text inputs, send buttons, and conversation windows remain readable and accessible without horizontal scroll issues[cite: 15].
* **Traceability:** RNF14[cite: 15].

---

## Epic 4: Administration & Knowledge Base

### US09: Administrator Login via JWT
* **As an** administrator,
* **I want to** log in securely using username and password,
* **So that** only authorized faculty staff can access the document management tools[cite: 10, 11].

#### Acceptance Criteria
1. The admin panel requires credentials to grant access[cite: 10, 11].
2. Upon successful authentication, the server returns a JWT token for securing subsequent administrative requests[cite: 13].
3. Invalid credentials return an HTTP 401 error message[cite: 10, 11].
* **Traceability:** RF09, RNF04[cite: 10, 11, 13].

---

### US10: Official Document Ingestion
* **As an** administrator,
* **I want to** upload and remove official faculty PDFs (calendars, study plans, regulations),
* **So that** the assistant’s knowledge base stays up to date[cite: 9, 11, 12].

#### Acceptance Criteria
1. An authenticated administrator can upload new institutional documents[cite: 11, 13].
2. The file list is updated with status information[cite: 11].
3. Deprecated documents can be deleted from active storage[cite: 11].
* **Traceability:** RF10, RNF04[cite: 11, 13].

---

### US11: Intent & Static Answer Management (CRUD)
* **As an** administrator,
* **I want to** create, edit, list, and delete custom intents with their keywords and static answers,
* **So that** I can quickly update recurrent announcements without re-training the whole AI system[cite: 11].

#### Acceptance Criteria
1. The dashboard provides full CRUD operations for intents[cite: 11].
2. Each intent supports triggering keywords and a Markdown static answer[cite: 11].
3. Saved changes take effect immediately on incoming queries[cite: 9, 11].
* **Traceability:** RF11[cite: 11].

---

### US12: Live Vector Re-indexing
* **As an** administrator,
* **I want to** trigger a knowledge base re-indexing action from the dashboard without stopping the backend server,
* **So that** students experience zero service downtime while new documents are indexed[cite: 11].

#### Acceptance Criteria
1. The dashboard provides a button to trigger re-indexing on demand[cite: 11].
2. Document chunking and vector embedding generation run in the background[cite: 11].
3. The system continues responding to student queries during the process without needing a server restart[cite: 11].
* **Traceability:** RF12, RNF04, RNF10[cite: 11, 13, 14].