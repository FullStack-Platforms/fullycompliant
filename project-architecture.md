compliancetracker/
├── frontend/         # React Frontend Application
│   ├── public/
│   ├── src/
│   ├── package.json
│   └── ... (Standard React project structure)
│
├── backend/          # Go Backend API Service
│   ├── cmd/
│   │   └── server/   # Main application entry point
│   │       └── main.go
│   ├── internal/     # Private application code
│   │   ├── api/      # HTTP handlers, routing, middleware
│   │   ├── auth/     # Authentication (JWT, password hashing, invite logic)
│   │   ├── compliance/ # Core business logic (controls, frameworks, status)
│   │   ├── config/   # Configuration loading (env vars, files)
│   │   ├── filestore/ # MinIO interaction logic
│   │   ├── models/   # Data structures (used across layers)
│   │   ├── secrets/  # Vault interaction logic
│   │   ├── ssp/      # SSP generation logic
│   │   └── store/    # Database interaction logic (interfaces & Postgres implementation)
│   ├── migrations/   # SQL migration files
│   ├── api/          # OpenAPI/Swagger specifications (optional)
│   ├── go.mod
│   ├── go.sum
│   └── Makefile      # Common development commands
│
├── docker-compose.yml # Docker Compose for local dev environment
├── .env.example       # Example environment variables
├── .gitignore
└── llm.md             # LLM Guidance