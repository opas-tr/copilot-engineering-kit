# AI Dev Template

> Copilot AI Template สำหรับ Senior Fullstack Developer  
> Stack: Java + Dropwizard + JDBI3 + PostgreSQL + React

---

## Overview

This template provides GitHub Copilot with the context it needs to generate code that follows the conventions and architecture of this project — as a senior developer would write it.

---

## Project Structure

```
ai-dev-template/
│
├─ .github/
│   └─ copilot-instructions.md   # Primary Copilot context file
│
├─ docs/
│   ├─ architecture.md           # System architecture and layer diagram
│   ├─ workflow.md                # Feature development workflow
│   ├─ backend-rules.md          # Java / Dropwizard / JDBI3 coding rules
│   ├─ frontend-rules.md         # React / Hooks coding rules
│   └─ database-rules.md         # PostgreSQL / Liquibase migration rules
│
├─ backend/                      # Java backend (Dropwizard)
│   ├─ src/main/java/            # Application source
│   ├─ resources/                # Configuration files
│   └─ migrations/               # Liquibase changelogs
│
├─ frontend/                     # React frontend
│   ├─ src/                      # Application source
│   └─ components/               # UI components
│
└─ README.md
```

---

## Tech Stack

| Layer    | Technology                  |
|----------|-----------------------------|
| Backend  | Java, Dropwizard, JDBI3     |
| Database | PostgreSQL, Liquibase        |
| Frontend | React, React Hooks           |
| IDE      | Visual Studio Code           |
| AI       | GitHub Copilot               |

---

## How Copilot Uses This Template

GitHub Copilot reads `.github/copilot-instructions.md` as its primary instruction file. The `docs/` folder provides deeper context about architecture, workflow, and coding rules for each layer.

| File | Purpose |
|------|---------|
| `.github/copilot-instructions.md` | Tells Copilot the tech stack, architecture, and coding rules |
| `docs/architecture.md` | Describes system layers and data flow |
| `docs/workflow.md` | Describes the step-by-step feature development process |
| `docs/backend-rules.md` | Java / Dropwizard / JDBI3 coding standards with examples |
| `docs/frontend-rules.md` | React / Hooks coding standards with examples |
| `docs/database-rules.md` | PostgreSQL schema design and Liquibase migration rules |

---

## Quick Start

1. Copy `.github/copilot-instructions.md` into your project's `.github/` folder
2. Copy the `docs/` folder into your project
3. Open the project in VS Code with GitHub Copilot enabled
4. Copilot will now generate code following your project's architecture and rules

---

## Contributing

When adding new rules or updating architecture:
- Update the relevant file in `docs/`
- Keep `.github/copilot-instructions.md` in sync with key rules
- Follow the existing Markdown formatting style
