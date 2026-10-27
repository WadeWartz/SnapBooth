# SnapBooth - Project Constitution
This document defines the core principles, technical standards, and development guidelines for the SnapBooth project. All team members and AI coding assistants must strictly adhere to these rules.

## 1. Core Principles 
1. **Security First:** Never commit API keys, secrets, or database credentials to the repository. All sensitive data must be stored in `.env` files.
2. **User Experience:** The application must be highly responsive. Camera operations must run smoothly on mobile devices (Guest) without lag.
3. **Real-time Interaction:** The Live Photo Wall must update instantly for the Host using WebSockets.
4. **AI as an Assistant:** AI (Groq API) is strictly used for intent extraction (returning JSON). The core logic (database queries, scoring, image processing) must be handled by our own Backend.
5. **No Local File Storage:** Never save uploaded images to the server's local disk. All images MUST be uploaded to Cloudinary, and only the returned URL should be saved in PostgreSQL.

## 2. Technical Stack & Architecture
*   **Frontend:** *[TO BE DETERMINED]* - The frontend framework (React, Next.js, etc.) is currently being evaluated. Rules for Frontend will be updated in this document once finalized. Until then, all frontend code must be modular and component-based.
*   **Backend Framework:** FastAPI (Python 3.10+).
*   **Database & ORM:** PostgreSQL + SQLAlchemy (Async) + `asyncpg` driver.
*   **Database Migrations:** Alembic.
*   **Real-time Server:** `python-socketio` (WebSockets).
*   **AI Service:** Groq API (Llama 3 model, enforcing JSON mode).
*   **Cloud Storage:** Cloudinary.
*   **Authentication:** JWT via `python-jose`, password hashing via `passlib[bcrypt]`.

## 3. Coding Standards 
1. **Backend Strictness:** Use Python type hints strictly. Use **Pydantic** models for all request/response data validation in FastAPI. Absolutely NO bare `dict` types for API payloads if a Pydantic model can be used.
2. **Asynchronous Python:** All database operations and external API calls (Cloudinary, Groq) in FastAPI MUST use `async def` and `await` to prevent blocking the server.
3. **Naming Conventions:**
    *   Python Variables & Functions: `snake_case`
    *   Python Classes & Pydantic Models: `PascalCase`
    *   Database Tables & Columns: `snake_case` (Plural for tables, e.g., `users`, `events`)
    *   Environment Variables: `UPPER_SNAKE_CASE`
4. **API Response Format:** All FastAPI successful responses must follow this consistent JSON structure:
   ```json
   { "success": true, "data": {}, "message": "Action completed" }