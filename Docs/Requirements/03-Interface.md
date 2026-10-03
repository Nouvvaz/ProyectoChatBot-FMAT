# 4. External Interface Requirements

This document defines the interface specifications for the FMAT UADY Virtual Assistant, covering user interfaces, hardware constraints, software integration points, and communication protocols.

---

## 4.1 User Interfaces (UI)

The system provides two distinct graphical presentation interfaces: an embeddable student-facing chat client and an authenticated administrative dashboard.

### 4.1.1 Student Conversational Widget

The student interface operates as an embeddable, lightweight web widget integrated into the official FMAT web portal.

- **Responsive Layout:** The interface adapts dynamically to desktop displays and mobile browser viewports[cite: 15].
- **Privacy Notice Banner:** A mandatory, visible banner informs the user that the session is anonymous and no conversation history is permanently retained[cite: 10].
- **Markdown Rendering Engine:** The message container parses Markdown syntax, rendering bold typography, ordered/unordered lists, and active hyperlinks directing users to official institutional forms and regulations.
- **Session Indicators:** Displays real-time visual feedback during inference latency ($\le 12$ seconds for RAG queries[cite: 12]) and alerts users upon automatic session expiration after 30 minutes of inactivity[cite: 9].

### 4.1.2 Administrative Dashboard

A secure, web-based management console accessible exclusively to authorized faculty personnel[cite: 10, 11].

- **Authentication View:** Username and password credential login interface gating access to management routes[cite: 10, 11].
- **Document Management Module:** Upload, inspect, and delete interfaces for official institutional PDF regulations and guidelines.
- **Intent Management Console:** CRUD table interface for managing custom intents, triggering keywords, and direct static responses.
- **Re-indexing Action Trigger:** Administrative control allowing live vector re-indexing with visual status indicators without stopping backend execution[cite: 11].

---

## 4.2 Hardware Interfaces

The platform requires no specialized proprietary hardware interfaces, operating over standard network architecture and consumer devices.

### 4.2.1 Server Infrastructure
- **Processor:** Multi-core x86_64 CPU (minimum 8 cores recommended) or dedicated CUDA-compatible GPU to maintain local LLM response latency $\le 12$ seconds[cite: 12].
- **RAM:** Minimum 16 GB to accommodate the containerized local model runtime, vector index, and application services concurrently[cite: 12, 14, 15].
- **Storage:** Solid-State Drive (SSD) with sufficient capacity for Docker images, vector database files, and uploaded institutional PDF archives[cite: 11, 14, 15].

### 4.2.2 Client Hardware
- Standard desktop, laptop, tablet, or smartphone devices equipped with modern web browsers capable of rendering CSS Grid/Flexbox and executing JavaScript[cite: 15].

---

## 4.3 Software Interfaces