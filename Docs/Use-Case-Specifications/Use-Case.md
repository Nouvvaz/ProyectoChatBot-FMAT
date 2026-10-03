# Use Case Specifications

This document outlines the main use cases for the FMAT UADY Virtual Assistant, showing how students and administrators interact with the system based on the project requirements[cite: 9, 10, 11].

---

## 1. System Actors

* **Student / General User:** A student or visitor who opens the chat widget to ask questions about school procedures, calendars, or faculty services without needing to log in[cite: 10, 15].
* **System Administrator:** An authorized staff or team member who logs in to upload official documents, edit intents, and refresh the knowledge base[cite: 10, 11].
* **Local RAG / AI Engine:** The internal system that searches official documents and generates answers locally using the language model[cite: 9, 14].

---

## 2. Use Case Summary Table

| Code | Use Case | Main Actor | Requirements | Priority |
| :---: | :--- | :--- | :--- | :---: |
| **UC01** | Start anonymous session and show privacy notice | Student / General User | RF01, RF06, RF08[cite: 9, 10] | High[cite: 9, 10] |
| **UC02** | Ask academic questions using local RAG | Student / General User | RF02, RF13, RF14, RF15, RNF01, RNF09[cite: 9, 11, 12, 14] | High[cite: 9, 11, 12, 14] |
| **UC03** | Get quick answer for a predefined intent | Student / General User | RF03, RF14, RNF01[cite: 9, 11, 12] | High[cite: 9, 12] |
| **UC04** | Route to official office contacts (fallback) | Student / General User | RF04, RF05, RNF09[cite: 9, 10, 14] | High[cite: 9, 10, 14] |
| **UC05** | Get guidance for external university services | Student / General User | RF16, RF14[cite: 11, 12] | Medium[cite: 11, 12] |
| **UC06** | End session and clear chat on inactivity | System (Automatic) | RF01, RF07, RNF05[cite: 9, 10, 13] | High[cite: 9, 10, 13] |
| **UC07** | Administrator login | System Administrator | RF09, RNF04[cite: 10, 11, 13] | High[cite: 10, 13] |
| **UC08** | Upload and manage official documents | System Administrator | RF10, RNF04[cite: 11, 13] | Medium[cite: 11] |
| **UC09** | Manage intents and quick answers (CRUD) | System Administrator | RF11, RNF04[cite: 11, 13] | Medium[cite: 11] |
| **UC10** | Re-index vector database | System Administrator | RF12, RNF04[cite: 11, 13] | High[cite: 11] |

---

## 3. Detailed Use Cases

### UC01: Start Anonymous Session and Show Privacy Notice
* **Actor:** Student / General User[cite: 10].
* **Description:** The user opens the chat widget to start asking questions without creating an account or logging in[cite: 10].
* **Preconditions:** The user visits the FMAT website on a computer or mobile phone[cite: 15].
* **Main Flow:**
  1. The user clicks on the chat widget on the page[cite: 10, 15].
  2. The widget opens and displays a clear privacy notice explaining that the chat is anonymous and no history is kept after closing[cite: 10].
  3. The backend creates a temporary session ID in memory without saving any personal information[cite: 10, 13].
  4. The assistant displays an initial greeting and is ready for questions[cite: 10].
* **Postconditions:** A temporary session is active with a 30-minute inactivity timer[cite: 9, 10].

---

### UC02: Ask Academic Questions Using Local RAG
* **Actors:** Student / General User, Local RAG / AI Engine[cite: 9, 10].
* **Description:** The student asks an academic question (e.g., re-enrollment, degree requirements, academic calendar, or social service) and receives an answer based on official documents[cite: 9, 12].
* **Preconditions:** The session is active and official FMAT documents are indexed[cite: 10, 11].
* **Main Flow:**
  1. The user types a question in natural language (in Spanish) and presses send[cite: 9, 15].
  2. The frontend sends the question via `POST /api/v1/chat/message`[cite: 11].
  3. The backend cleans and sanitizes the input to protect against injection attacks[cite: 13].
  4. The message is temporarily stored in the session history[cite: 10].
  5. The RAG system searches the local vector store for relevant excerpts from official FMAT files[cite: 9, 11].
  6. The local model builds an answer based only on those documents in 12 seconds or less[cite: 9, 12, 14].
  7. The response is returned in Markdown format with bold text, bullet points, and links to official forms or rules[cite: 11, 12].
  8. The user sees the formatted response in the chat[cite: 11].
* **Alternative Flows:**
  * **Low confidence or missing information:** If the system is not sure of the answer or cannot find it in the files, it triggers **UC04** instead of guessing[cite: 9, 10, 14].
* **Postconditions:** The inactivity countdown restarts to 30 minutes[cite: 9].

---

### UC03: Get Quick Answer for a Predefined Intent
* **Actor:** Student / General User[cite: 9, 10].
* **Description:** The user asks a common question that maps directly to a saved intent (such as asking for a specific lab location)[cite: 9].
* **Preconditions:** Active session and registered intents in the system[cite: 9, 10, 11].
* **Main Flow:**
  1. The user asks a direct question (e.g., "Where is the lab located?")[cite: 9].
  2. The system classifies the message into an intent (like `UbicacionLaboratorio`)[cite: 9].
  3. The backend immediately returns the predefined answer in 5 seconds or less without running the heavy local model[cite: 9, 12].
  4. The answer is displayed in Markdown format[cite: 11].
* **Postconditions:** The message and answer are appended to the temporary session log[cite: 10].

---

### UC04: Route to Official Office Contacts (Fallback)
* **Actor:** Student / General User[cite: 9, 10].
* **Description:** The bot politely handles questions that are outside of FMAT topics or where it does not have enough certainty to answer safely[cite: 9, 10].
* **Preconditions:** The backend received a user question[cite: 11].
* **Main Flow:**
  1. The backend evaluates the query[cite: 9, 10].
  2. The system detects that the question is either not about FMAT or has a similarity score below the minimum threshold[cite: 9, 10].
  3. The bot sends a predefined fallback message stating it does not have the information[cite: 9, 10].
  4. The bot provides direct email and contact details for Control Escolar or Secretaría Académica[cite: 9, 10].
* **Postconditions:** The bot prevents false answers (hallucinations) and gives students a direct path to human staff[cite: 9, 10, 14].

---

### UC05: Get Guidance for External University Services
* **Actor:** Student / General User[cite: 10, 12].
* **Description:** The user asks about university services not handled directly by FMAT's Control Escolar (such as IMSS insurance, English courses at CIL, student IDs, or external scholarships)[cite: 12].
* **Preconditions:** Active chat session[cite: 10].
* **Main Flow:**
  1. The user asks about a general university procedure[cite: 12].
  2. The system detects that the topic belongs to another department[cite: 12].
  3. The bot gives general step-by-step guidance and provides direct links and contact info for the responsible office[cite: 11, 12].
* **Postconditions:** The student is redirected to the right university department[cite: 12].

---

### UC06: End Session and Clear Chat on Inactivity
* **Actor:** System (Automatic)[cite: 9].
* **Description:** The system automatically cleans up the conversation after 30 minutes of inactivity or when the browser closes[cite: 9].
* **Preconditions:** An active temporary session exists in memory[cite: 10].
* **Main Flow:**
  1. The user does not interact for 30 minutes, or closes the browser tab[cite: 9].
  2. The system detects the timeout or disconnect[cite: 9].
  3. The backend deletes the temporary session data and message history from memory[cite: 9, 10].
  4. No student data, names, or messages are written to persistent server logs[cite: 10, 13].
* **Postconditions:** Server memory is released and student privacy is protected[cite: 9, 10, 13].

---

### UC07: Administrator Login
* **Actor:** System Administrator[cite: 10, 11].
* **Description:** An administrator logs in with username and password to manage system data[cite: 10, 11].
* **Preconditions:** Admin visits the management URL over HTTPS[cite: 10, 11, 13].
* **Main Flow:**
  1. The administrator enters their username and password[cite: 10, 11].
  2. The backend checks credentials securely[cite: 10, 11].
  3. The server responds with a JWT authentication token[cite: 13].
  4. The admin interface unlocks access to document and intent tools[cite: 10, 11].
* **Alternative Flows:**
  * **Wrong credentials:** The system shows an error message and denies access[cite: 10, 11].
* **Postconditions:** The administrator has a valid JWT token to use protected endpoints[cite: 10, 11, 13].

---

### UC08: Upload and Manage Official Documents
* **Actor:** System Administrator[cite: 11].
* **Description:** The administrator uploads new or updated institutional PDFs (e.g., calendars, study plans, guides)[cite: 9, 11, 12].
* **Preconditions:** Admin is logged in with a valid JWT token[cite: 10, 11, 13].
* **Main Flow:**
  1. The administrator navigates to the Documents tab[cite: 11].
  2. The admin selects and uploads an official PDF file[cite: 11].
  3. The backend saves the document in the server storage[cite: 11].
  4. The dashboard updates the file list and notifies the admin to run re-indexing[cite: 11].
* **Alternative Flows:**
  * **Delete document:** The admin selects an outdated PDF and deletes it from the list[cite: 11].
* **Postconditions:** The document folder has the updated official files[cite: 11].

---

### UC09: Manage Intents and Quick Answers (CRUD)
* **Actor:** System Administrator[cite: 11].
* **Description:** The administrator manages predefined intents, keywords, and static responses[cite: 11].
* **Preconditions:** Admin is logged in with a valid JWT token[cite: 10, 11, 13].
* **Main Flow:**
  1. The administrator enters the Intents management view[cite: 11].
  2. The admin can create a new intent, update keywords, edit the Markdown answer, or delete an old one[cite: 11].
  3. The backend saves the updated intent configuration[cite: 11].
* **Postconditions:** The bot immediately uses the new intent settings for incoming messages[cite: 9, 11].

---

### UC10: Re-Index Vector Database
* **Actors:** System Administrator, Local RAG / AI Engine[cite: 11].
* **Description:** The administrator triggers vector database re-indexing so new documents can be searched without rebooting the server[cite: 11].
* **Preconditions:** Admin is logged in and documents were modified[cite: 10, 11, 13].
* **Main Flow:**
  1. The admin clicks the "Re-index Knowledge Base" button in the dashboard[cite: 11].
  2. The backend splits the active documents into chunks and calculates vector embeddings in the background[cite: 11].
  3. The vector database updates smoothly without restarting the backend service[cite: 11].
  4. The panel displays a confirmation message when finished[cite: 11].
* **Postconditions:** The chat engine answers future questions using the latest document content[cite: 9, 11].