Automated API Testing & Auth Framework (Postman)
 Project Overview
This repository contains a high-performance **Postman Collection** and **Environment Framework** designed for an Applicant Tracking System (ATS).
It demonstrates an automated approach to managing API lifecycles, focusing on secure JWT handling and RESTful best practices.

Key Technical Features
- **Dynamic JWT Management:** Automated extraction and injection of Bearer tokens using Post-Response scripts.
- **Local Session Validation:** A custom JavaScript Pre-request script that decodes JWT payloads to check for expiration *before* requests are sent.
- **Environment Agnostic:** Fully decoupled variables (`{{baseurl}}`) allowing seamless switching between Local, Staging, and Cloud environments.
- **REST Compliance:** Standardised HTTP methods (POST/GET/PUT) to ensure architectural integrity.

Evolution:  Legacy vs. 2026 Professional Framework
During the development of this project, I identified several legacy "quick-fix" patterns from 2019-2026 and refactored them into a modern automation suite.
 1. Authentication Lifecycle
*   **Practice:** Tokens were manually copied from login responses and hardcoded into headers.
*   **Refactor:** Implemented **Tests Tab Scripts** to automatically capture `data.token` and update the `{{Token}}` environment variable globally.

2. Pre-Request Security Layer
*   ** Practice:** Requests were sent blindly, often resulting in 401 Unauthorized errors due to expired sessions.
*   **Refactor:** Added a **Collection-level Pre-request Script**. This script decodes the Base64 JWT payload and compares the `exp` claim to the current system time. It warns the user in the console if a re-login is required, saving significant debugging time.
3. Structural Integrity
*   **Practice:** Some "Create" actions incorrectly used `GET` methods with JSON bodies.
*   **Refactor:** Corrected all endpoints to follow **REST standards**, ensuring "Create" actions use `POST` and "Update" actions use `PUT/PATCH`.
How to Use
1.  **Import Files:** Download the `collection.json` and `environment.json` from this repo.
2.  **Select Environment:** Ensure the `Production_Mock_API` environment is active.
3.  **Authentication:** Run the `Sign IN` or `Sign UP` request first. This will automatically populate your `{{Token}}` variable.
4.  **Protected Routes:** All other requests (e.g., "Add Client") will now work automatically using the stored token.
Tech Stack
- **Tooling:** Postman v11+
- **Scripting:** JavaScript (Postman Sandbox)
- **Architecture:** RESTful API
- **Auth:** JWT (JSON Web Token) / Bearer Authentication
*Note: This project uses a mock API (ReqRes.in) for demonstration purposes to protect proprietary infrastructure and data.*
