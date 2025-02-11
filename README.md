# Axum Askama Template

This is a Rust-based web application template built with [Axum](https://github.com/tokio-rs/axum) for the web
framework and [Askama](https://github.com/rinja-rs/askama) for templating. It
follows a structured architecture inspired by "[Zero to Production in
Rust](https://www.zero2prod.com/index.html)" to promote maintainability,
testability, and scalability.

## Features

* **Axum Web Framework:**  A fast and ergonomic web framework for Rust.
* **Askama Templating:**  A compile-time HTML templating engine for Rust, ensuring type safety and performance.
* **Structured Architecture:**  A layered architecture with clear separation of concerns, making the codebase easier to understand and maintain.
* **Configuration Management:**  Uses `config` crate for managing application settings with support for base, local, and production configurations.
* **Database Integration:**  Uses `sqlx` for asynchronous database interactions with PostgreSQL.
* **Telemetry:**  Uses `tracing` and `tracing-bunyan-formatter` for structured logging and tracing.
* **Middleware:**  Includes request logging middleware using `tower-http`.
* **Dependency Injection:**  Uses Axum's `with_state` for dependency injection, making it easy to provide shared state to route handlers.
* **Docker Support:**  Includes a `Dockerfile` for easy containerization.
* **Justfile:**  Includes a `Justfile` for common development tasks.
* **`cargo-generate` Template:**  Easily generate new projects from this template using `cargo-generate`.

## Getting Started

### Prerequisites

* Rust toolchain (stable or nightly)
* PostgreSQL database
* Docker (optional, for containerization)
* Just (optional, for task running)
* [`cargo-generate`](https://crates.io/crates/cargo-generate) (recommended for generating new projects)
* [`bunyan`](https://crates.io/crates/bunyan) (optional, for formatting console logs)

### Configuration

1. **Database:**

* Create a PostgreSQL database.
* Update the database connection string in `config/base.toml` (and `local.toml` or `production.toml` as needed).

2. **Environment Variables:**

* Set any required environment variables (e.g., for email sending).

### Creating a New Project

1. **Install `cargo-generate`:**

```bash
cargo install cargo-generate
```

2. **Generate a new project:**

```bash
cargo generate kristoferssolo/axum-template
```

### Running the Application

1. **Navigate to the new project directory:**

```bash
cd <project_name>
```

2. **Initialize the database:**

```bash
bash scripts/init_db
```

3. **Run the application:**

```bash
cargo run
```

Or, if you have `just` installed:

```bash
just dev
```

4. **Access the application:**

Open your browser and navigate to `http://localhost:8000` (or the configured port).

### Running Tests

```bash
cargo test
```

## Directory Structure

```bash
├── Cargo.toml
├── config/                 # Handles loading and merging configuration files.
│   ├── base.toml           # Base configuration
│   ├── local.toml          # Local development overrides
│   └── production.toml     # Production configuration overrides
├── Dockerfile
├── justfile
├── migrations/             # Database migrations
├── README.md               # This file
├── scripts/                # Utility scripts
│   └── init_db             # Script to initialize the database
├── src/
│   ├── config/             # Configuration loading and management
│   │   ├── database.rs     # Database connection settings
│   │   ├── environment.rs  # Environment-related settings (e.g., enum for environment type)
│   │   └── application.rs  # Application-specific settings
│   ├── domain/             # Defines the core business logic and data structures.
│   ├── errors/             # Custom error types
│   ├── lib.rs             
│   ├── main.rs
│   ├── middleware/         # Custom Axum middleware
│   ├── models/             # Defines the database models (entities).
│   ├── repositories/       # Provides an abstraction layer for data access.
│   ├── routes/             # Defines the Axum route handlers.
│   ├── services/           # Implements the business logic of the application.
│   └── startup.rs          # Application startup and configuration
├── templates/              # Askama templates
├── tests/                  # Integration tests
│   └── api/                # API-specific tests
│       ├── health_check.rs # Tests for the health check endpoint
│       └── helpers.rs      # Helper functions for API tests
```

### Key Components

* **`config`:**  Handles loading and merging configuration files.
* **`domain`:**  Defines the core business logic and data structures.
* **`models`:**  Defines the database models (entities).
* **`repositories`:**  Provides an abstraction layer for data access.
* **`services`:**  Implements the business logic of the application.
* **`routes`:**  Defines the Axum route handlers.
* **`telemetry`:**  Sets up tracing and logging.
* **`templates`:**  Contains the Askama templates.

## Contributing

Contributions are welcome! Please submit a pull request with your changes.

## License

This project is licensed under the [MIT License](LICENSE).
