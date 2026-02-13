### **Authentication vs. Authorization**

*   **Authentication ("Who are you?")**: The process of assigning an identity to a subject. It answers the question of who a user is within a given context (platform, OS, etc.).
*   **Authorization ("What can you do?")**: The process of determining the permissions and capabilities of that authenticated subject within the context.

---

### **1. Historical Context of Authentication**

The evolution of authentication was driven by the need to scale trust beyond personal circles.

*   **Pre-Industrial**: **Implicit Trust**. Identity was based on recognition by the community (e.g., a village elder vouching for someone). Deals were sealed with handshakes.
*   **Medieval**: **Seals (Possession)**. As society grew, implicit trust failed to scale. Wax seals were introduced as physical tokens of identity ("something you have") but were prone to forgery.
*   **Industrial Revolution**: **Passphrases (Knowledge)**. The telegraph introduced the need for secure message validation using pre-agreed passphrases or shared secrets ("something you know").
*   **Digital Age (Mid-20th Century)**: **Passwords**. MIT’s Project MAC introduced passwords for multi-user systems. Initially stored in plain text, a printing accident led to the realization that secure storage (hashing) was necessary.
*   **1970s**: **Public Key Infrastructure (PKI)**. Diffie and Hellman introduced asymmetric cryptography (public/private keys), allowing secure exchange over untrusted mediums.
*   **1990s**: **Multi-Factor Authentication (MFA)**. Combined three principles:
    1.  Something you **know** (password).
    2.  Something you **have** (card/token).
    3.  Something you **are** (biometrics like fingerprints).
*   **Modern/Future**: Includes OAuth 2.0, JWT, Zero Trust, and emerging tech like decentralized identity (blockchain) and post-quantum cryptography.

---

### **2. Core Components**

Three technical components are essential to modern authentication flows:

#### **A. Sessions**
*   **Why**: HTTP is **stateless** by design, meaning it doesn't remember past requests. Interactive web apps (e.g., shopping carts) need **stateful** interactions.
*   **How it works**:
    1.  User logs in.
    2.  Server creates a unique **Session ID** and stores user data in a persistent store (Database or Redis).
    3.  Session ID is sent to the client as a **Cookie**.
    4.  Client sends the cookie with every subsequent request, allowing the server to look up the user context.

#### **B. JSON Web Tokens (JWT)**
*   **Why**: Sessions struggle with scalability in distributed systems (latency in replicating session data across regions).
*   **Concept**: A **stateless** mechanism where user data is self-contained in the token.
*   **Structure**:
    1.  **Header**: Metadata (e.g., algorithm).
    2.  **Payload**: Data/Claims (User ID, Expiry, Roles).
    3.  **Signature**: Verifies integrity using a secret key.
*   **Pros**: No server-side storage required, scalable, portable.
*   **Cons**:
    *   **Revocation**: Difficult to invalidate a token before it expires without changing the secret key (which logs everyone out).
    *   **Hybrid Approach**: Storing a "blacklist" of revoked tokens in a database solves this but reintroduces statefulness.

#### **C. Cookies**
*   **Definition**: A mechanism for the server to store a piece of information in the client's browser.
*   **Function**: Browsers automatically send cookies back to the specific server with every request. Used to transport Session IDs or Tokens securely.

---

### **3. Major Types of Authentication**

#### **A. Stateful Authentication (Session-Based)**
*   **Workflow**: Server verifies credentials $\rightarrow$ creates session in Redis $\rightarrow$ sends Session ID in an HTTP-only cookie.
*   **Pros**: Centralized control, easy to revoke access instantly (just delete the session from Redis).
*   **Cons**: Harder to scale in distributed architectures.
*   **Best Use**: Standard web applications (SaaS).

#### **B. Stateless Authentication (Token-Based/JWT)**
*   **Workflow**: Server verifies credentials $\rightarrow$ signs a JWT $\rightarrow$ sends to client. Client sends JWT in the `Authorization` header for requests.
*   **Pros**: Highly scalable, ideal for microservices and mobile apps.
*   **Cons**: Token revocation is complex.

#### **C. API Keys**
*   **Concept**: A generated secret string used for **machine-to-machine** communication (e.g., a script accessing OpenAI's API).
*   **Workflow**: Client includes the API key in the request header. No login form or human interaction involved.
*   **Best Use**: Programmatic access to a server.

#### **D. OAuth 2.0 & OpenID Connect (OIDC)**
*   **The Problem**: "Delegation." How to let one app (e.g., a travel site) access resources on another (e.g., Gmail) without sharing the user's password.
*   **OAuth 2.0 (Authorization)**:
    *   Uses **Access Tokens** instead of passwords to grant specific, limited permissions.
    *   **Flows**: Supports different flows for servers, browsers, and devices (e.g., Smart TVs).
*   **OpenID Connect (Authentication)**:
    *   Built on top of OAuth 2.0 to solve identity. Adds an **ID Token** (JWT).
    *   Enables "Sign in with Google/Facebook" features.
*   **Best Use**: Third-party integrations and social logins.

---

### **4. Authorization**

*   **Definition**: Controlling access to specific resources based on the user's identity.
*   **RBAC (Role-Based Access Control)**:
    *   Users are assigned roles (e.g., Admin, Member, Moderator).
    *   Permissions are attached to roles (e.g., Admins can `delete`, Members can only `read`).
    *   **Workflow**: Server checks the user's role during the request and returns `403 Forbidden` if they lack permission.

---

### **5. Security Best Practices**

#### **Generic Error Messages**
*   **Risk**: Specific messages like "User not found" or "Incorrect password" allow attackers to enumerate valid usernames.
*   **Solution**: Always use generic messages like "Invalid credentials" or "Authentication failed".

#### **Defending Against Timing Attacks**
*   **Risk**: If the server rejects an invalid username quickly but takes longer to verify a password for a valid username (due to hashing time), attackers can measure the delay to guess which users exist.
*   **Solution**:
    *   Use constant-time comparison operations.
    *   Simulate delays (e.g., `setTimeout`) so all requests take the same amount of time regardless of the outcome.
