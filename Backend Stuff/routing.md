### **I. Core Concept: What is Routing?**

*   **The "What" vs. The "Where"**:
    *   **HTTP Methods (The What):** Express the intent or action (GET, POST, DELETE, etc.).
    *   **Routing (The Where):** Expresses the address or resource you want to perform that action on.
*   **Definition**: Routing is the process of mapping **URL parameters** (the address) + the **HTTP Method** (the action) to a specific **Server-Side Handler** (logic/function).
*   **The Goal**: To guide a request to the correct set of instructions (database operations, business logic) to return the appropriate data.

---

### **II. The Routing Mechanism**

*   **The Unique Key**: The server uses the combination of the **Method** and the **Route Path** as a unique key to find the correct handler.
    *   *Example:* A `GET` request to `/api/books` is distinct from a `POST` request to `/api/books`. Even though the route is the same, the method differentiates them, so they never clash.

---

### **III. Types of Routing**

#### **1. Static Routes**
*   **Definition**: Routes defined by a constant string with no variable parts.
*   **Behavior**: They always point to the same resource and return the same *kind* of response structure.
*   **Example**: `/api/books` is a fixed string. Nothing in the URL changes between requests.

#### **2. Dynamic Routes (Path Parameters)**
*   **Definition**: Routes that contain variable segments (Dynamic Parameters) to identify specific resources.
*   **Syntax**: Commonly denoted by a colon (e.g., `/api/users/:id`). The server treats the part after the slash as a variable.
*   **Usage**: Used to fetch details of a specific entity based on a unique identifier (ID).
*   **Handling**: The server extracts the string value from the URL (e.g., `123` from `/api/users/123`) and injects it into the handler logic to query the database.
*   **Data Type**: Route parameters are always treated as **strings**, even if they look like numbers.
*   **Purpose**: Provides a human-readable, semantic way to identify resources (e.g., "Get me the user with ID 123").

---

### **IV. Query Parameters**

*   **Definition**: Key-value pairs added to the end of a URL after a question mark `?` (e.g., `/api/search?query=value`).
*   **Purpose**: To send metadata or user-defined values to the server, specifically for **GET requests**.
    *   *Context:* POST/PUT requests have a "Body" to send data. GET requests do not have a body, so Query Params are the standard way to pass inputs.
*   **Difference from Path Params**:
    *   **Path Params**: Used for **Semantic Identity** (identifying *which* resource).
    *   **Query Params**: Used for **Modifying the Response** (filtering, sorting, searching).
*   **Common Use Cases**:
    *   **Search**: Passing a search string (`?q=javascript`).
    *   **Pagination**: Breaking large datasets into chunks. The server returns metadata (current page, total pages) and the client requests the next chunk using params like `?page=2&limit=20`.
    *   **Sorting**: Specifying order (e.g., `?sort=asc`).

---

### **V. Nested Routes**

*   **Concept**: structuring routes hierarchically to express relationships between resources.
*   **Semantic Meaning**: It allows you to drill down from a parent resource to a child resource.
*   **Example Flow**:
    1.  `/api/users`: Fetch all users.
    2.  `/api/users/123`: Fetch specifically user 123.
    3.  `/api/users/123/posts`: Fetch all posts belonging *only* to user 123.
    4.  `/api/users/123/posts/456`: Fetch specifically post 456 that belongs to user 123.
*   **Why use it?**: It is a standard REST API practice to keep endpoints logical and readable.

---

### **VI. Route Versioning & Deprecation**

*   **The Problem**: Requirements change over time (e.g., a mobile app needs a different data format than the web app), but changing an existing API breaks current clients.
*   **The Solution**: Versioning the route (e.g., `/api/v1/products` vs `/api/v2/products`).
*   **Workflow**:
    1.  Create `v2` with the new structure while keeping `v1` active.
    2.  **Deprecate** `v1`: Inform engineers/clients that `v1` will be removed in the future.
    3.  **Migration Window**: Allow time for clients to switch their code to `v2`.
    4.  Remove `v1` once migration is complete.
*   **Benefit**: Allows breaking changes without disrupting the live application.

---

### **VII. Catch-All Routes**

*   **Definition**: A route (often denoted by `*`) placed at the very end of the routing logic.
*   **Purpose**: To handle requests that do **not** match any of the defined routes above it.
*   **Behavior**: Instead of the server crashing or sending a generic error, the Catch-All handler returns a user-friendly "404 Not Found" message, informing the client that the requested endpoint does not exist.
