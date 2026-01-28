<!--
SYNC IMPACT REPORT
==================
Date: 2025-01-28
Action: Initial Constitution Creation (v0.0.0 → v1.0.0)

VERSION CHANGE: 
  • Old: N/A (from template)
  • New: 1.0.0 (MAJOR release - initial ratification)
  • Rationale: First complete constitution for ContosoDashboard; establishes baseline principles, technical standards, and development workflow

PRINCIPLES CREATED (5/5):
  ✅ I. Spec-Driven Development
  ✅ II. Service-Based Architecture
  ✅ III. Authorization & Security (NON-NEGOTIABLE)
  ✅ IV. Infrastructure Abstraction & Cloud Migration Path
  ✅ V. Separation of Concerns & Clean Architecture

SECTIONS CREATED:
  ✅ Core Principles (5 principles)
  ✅ Technical Stack & Standards (6 technology requirements)
  ✅ Development Workflow (4 workflow standards)
  ✅ Quality Gates (Implementation & Merge gates + Architectural Constraints)
  ✅ Governance (Amendment process, validation, guidance)

TEMPLATES VALIDATION:
  ✅ spec-template.md - Aligned (user scenarios, acceptance criteria, independent testability)
  ✅ plan-template.md - Aligned (includes Constitution Check gate)
  ✅ tasks-template.md - Aligned (user story organization, independent tasks)
  ✅ checklist-template.md - Aligned (quality validation across domains)

DEPENDENT FILES - NO UPDATES REQUIRED:
  ✅ .github/agents/*.md - Already reference constitution validation
  ✅ .github/prompts/*.md - Already guide agents through workflow
  ✅ .specify/scripts/* - Automate workflow enforcement
  ✅ README.md - Documentation already reflects constitutional principles

VALIDATION RESULTS:
  ✅ No unresolved placeholder tokens
  ✅ All 5 principle slots filled
  ✅ All dates in ISO format (YYYY-MM-DD)
  ✅ Principles are declarative and testable
  ✅ Version string matches: 1.0.0
  ✅ Ratification date: 2025-01-28
  ✅ Last amended: 2025-01-28

DEFERRED ITEMS: None

NEXT STEPS:
  1. Commit constitution with suggested message
  2. Begin feature development using /speckit.specify workflow
  3. All features will be validated against Constitution Check in planning phase
-->

# ContosoDashboard Constitution

## Core Principles

### I. Spec-Driven Development

Every feature MUST start with a comprehensive written specification before any code is written. Specifications MUST include user scenarios, acceptance criteria, and architecture decisions. All specifications MUST be stored in the `specs/[###-feature-name]/` directory following the standard template. Specifications cannot be purely internal or organizational—each feature MUST deliver measurable user value.

### II. Service-Based Architecture

All business logic MUST be implemented as injected services (IUserService, ITaskService, etc.). Service layer MUST handle all authorization checks and prevent IDOR vulnerabilities. Data access MUST be encapsulated through Entity Framework Core with models and relationships defined in the Data layer. No direct controller/page access to database context.

### III. Authorization & Security (NON-NEGOTIABLE)

Authorization enforcement is mandatory on all protected pages using `[Authorize]` attributes. Role-Based Access Control (RBAC) MUST follow the four-tier hierarchy: Administrator > ProjectManager > TeamLead > Employee. Service layer MUST validate user permissions before data access—authorization checks cannot be optional. IDOR protection MUST be implemented by verifying user membership/ownership at service layer.

### IV. Infrastructure Abstraction & Cloud Migration Path

All infrastructure dependencies (database, file storage, identity) MUST be abstracted behind interfaces enabling local/cloud switching. Training implementations MUST work offline: LocalDB/SQLite for databases, local filesystem for file storage, cookie-based mock auth. Production migration requires only implementation swaps via dependency injection—no business logic changes.

### V. Separation of Concerns & Clean Architecture

Project structure MUST follow clear layering: Models (entities) → Data (DbContext/EF) → Services (business logic) → Pages/Razor Components (UI). Cross-cutting concerns (logging, error handling) MUST be handled in middleware or service decorators. No business logic in page code-behind. UI components MUST be stateless where possible.

## Technical Stack & Standards

**Framework & Language**: ASP.NET Core 8.0 with C# required. Blazor Server for interactive UI components.

**Database**: SQLite for development; Entity Framework Core 8.0 for ORM. Production: Azure SQL Database (implementation swap only).

**Authentication/Authorization**: Cookie-based mock authentication for training. Production: Microsoft Entra ID (Azure AD) with OAuth 2.0/OpenID Connect.

**UI Framework**: Blazor Server with Bootstrap 5.3 for styling. No client-side SPA frameworks required for this project.

**File Storage**: Local filesystem outside `wwwroot` for training. Production: Azure Blob Storage with interface abstraction.

**Database Migrations**: Entity Framework Code-First approach. Migrations MUST be versioned and committed. `dotnet-ef` CLI required for migration management.

## Development Workflow

**Spec-Driven Cadence**: Features follow the workflow: Specify → Clarify → Plan → Tasks → Checklists → Implement.

**Branch Naming**: `[###-feature-name]` format where `###` is a sequential number (e.g., `1-document-upload`). Branch MUST correspond to spec number.

**Commit Messages**: MUST reference feature number and include summary. Example: `feat(1-document-upload): implement file upload endpoint`.

**Code Review**: All PRs MUST include reference to feature spec and validation against constitution. Code that bypasses service layer, skips authorization checks, or violates architectural boundaries MUST be rejected.

**Testing**: Service layer unit tests REQUIRED for all new business logic. Integration tests REQUIRED for cross-service interactions and authorization flows. `[Authorize]` attribute enforcement MUST be tested.

**Database Updates**: Always use migrations. Direct schema changes are prohibited. Seeded data changes MUST be documented in migration comments.

## Quality Gates

**Mandatory Before Implementation**:
- ✅ Specification approved and in `specs/[###]/spec.md`
- ✅ Constitution Check passed (no architectural violations)
- ✅ Plan.md with data model and contracts generated
- ✅ Tasks.md with granular development tasks

**Mandatory Before Merge**:
- ✅ All tests passing (unit + integration)
- ✅ All checklists (UX, security, testing, performance) completed
- ✅ Code review approved with constitutional compliance
- ✅ No IDOR vulnerabilities (authorization verified at service layer)
- ✅ Documentation updated (README, spec completion)

**Architectural Constraints**:
- Service injection is REQUIRED; no tight coupling
- Authorization checks MUST be in service layer, not pages
- Infrastructure abstractions MUST be honored (no hardcoding implementations)
- Database access ONLY through DbContext
- No direct SQL queries without EF-Core wrapper

## Governance

This constitution supersedes all other documentation and practices. All feature development MUST comply with these principles. Constitution violations MUST be documented and justified in PR comments with explicit sign-off from project lead.

**Amendment Process**: Constitution changes require a dedicated amendment spec (`constitution-amendment.md`) with ratification date, version bump (semantic versioning), and impact assessment on existing features and templates.

**Compliance Validation**: The `speckit.constitution` agent MUST validate all feature specs, plans, and implementation against this constitution before approval.

**Guidance Documentation**: Runtime development guidance lives in `.specify/` scripts and templates. Constitution defines principles; templates define structure; scripts automate workflow.

---

**Version**: 1.0.0 | **Ratified**: 2025-01-28 | **Last Amended**: 2025-01-28
