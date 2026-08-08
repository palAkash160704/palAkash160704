# Engineering Standards Handbook

> [!NOTE]
> This document establishes the core engineering practices, conventions, and operational standards for all repositories under this portfolio. By adhering to these guidelines, all projects maintain production-grade reliability, security, and consistent architecture.

---

## 1. Folder Organization
Maintain a predictable directory structure for all services to reduce cognitive load.
```text
├── .github/          # CI/CD workflows, PR templates, issue templates
├── src/              # Source code (or `app/`, `core/`)
│   ├── api/          # Route controllers and endpoints
│   ├── models/       # Data schemas (Pydantic, SQLAlchemy)
│   ├── services/     # Business logic and external integrations
│   └── utils/        # Shared helper functions
├── tests/            # Unit, integration, and E2E tests
├── docs/             # Architecture diagrams and API specs
├── docker/           # Dockerfiles and compose configurations
├── .env.example      # Template for environment variables
├── .gitignore        # Standardized ignore file
├── README.md         # Project entrypoint
└── LICENSE           # Legal licensing
```

## 2. Naming Convention
- **Repositories:** PascalCase (`TripAI`) or kebab-case (`system-design`).
- **Directories:** kebab-case (`api-routes/`).
- **Files:** snake_case for Python (`data_loader.py`), kebab-case for TS/JS/React (`user-profile.tsx`).
- **Classes:** PascalCase (`UserRepository`).
- **Functions/Variables:** snake_case for Python (`get_user_data`), camelCase for TS/JS (`getUserData`).
- **Constants:** UPPER_SNAKE_CASE (`MAX_RETRY_COUNT`).

## 3. Coding Style
- **Python:** Strictly enforce PEP-8 using `Ruff` or `Black`. Enforce type hints on all function signatures.
- **JavaScript/TypeScript:** Strictly enforce `Prettier` and `ESLint`. Use strict typing (`strict: true` in `tsconfig.json`).
- **General:** Maximum line length of 100 characters. Avoid deeply nested conditionals (favor early returns).

## 4. Git Commit Convention
Follow [Conventional Commits](https://www.conventionalcommits.org/).
- `feat:` A new feature.
- `fix:` A bug fix.
- `docs:` Documentation only changes.
- `style:` Changes that do not affect code meaning (formatting, missing semi-colons, etc).
- `refactor:` Code change that neither fixes a bug nor adds a feature.
- `perf:` A code change that improves performance.
- `test:` Adding missing or correcting existing tests.
- `chore:` Changes to the build process or auxiliary tools (e.g., dependency updates).
*Example:* `feat(auth): implement JWT token rotation mechanism`

## 5. Pull Request Convention
- PRs must address a single concern or feature.
- PR titles must follow the Git Commit Convention.
- Every PR must include a description detailing *Why* the change was made, *How* it was implemented, and *How* it was tested.
- PRs cannot be merged until CI/CD pipelines pass successfully.

## 6. Branch Naming
- **Features:** `feature/<issue-id>-<short-description>` (e.g., `feature/12-add-redis-cache`)
- **Bug Fixes:** `bugfix/<issue-id>-<short-description>`
- **Hotfixes:** `hotfix/<issue-id>-<short-description>` (for production emergencies)
- **Releases:** `release/v<major>.<minor>.<patch>`

## 7. Issue Labels
Standardize issue tracking using colored labels:
- `bug` (Red): Something isn't working.
- `enhancement` (Cyan): New feature or request.
- `documentation` (Blue): Improvements or additions to docs.
- `good first issue` (Purple): Good for newcomers.
- `security` (Dark Red): Vulnerability fixes.
- `tech-debt` (Yellow): Refactoring or code cleanup.

## 8. Versioning
Strictly adhere to [Semantic Versioning (SemVer)](https://semver.org/).
- **MAJOR (`1.x.x`):** Incompatible API changes.
- **MINOR (`x.1.x`):** Backwards-compatible functionality additions.
- **PATCH (`x.x.1`):** Backwards-compatible bug fixes.

## 9. Documentation Rules
- Every public API, class, and complex function MUST have a docstring or JSDoc comment.
- Keep the `README.md` updated using the Universal Repository Template.
- Document architectural decisions using Architecture Decision Records (ADRs) stored in `docs/adr/`.

## 10. Testing Standards
- **Unit Tests:** Must test business logic in isolation. Minimum coverage target: **80%**.
- **Integration Tests:** Must verify interactions between services (e.g., Database, External APIs).
- **E2E Tests:** Must verify critical user journeys.
- **Frameworks:** `pytest` (Python), `Jest`/`Vitest` (JS/TS).

## 11. CI/CD Standards
- All commits pushed to PRs must automatically trigger the CI pipeline.
- CI pipelines must execute:
  1. Linter (`Ruff` / `ESLint`)
  2. Type Checker (`mypy` / `tsc`)
  3. Security Scanner (`Bandit` / `npm audit`)
  4. Test Suite (`pytest` / `Vitest`)
- CD pipelines deploy to staging automatically on merge to `main`, and to production upon manual release tagging.

## 12. GitHub Actions
- Keep workflows modular by utilizing composite actions.
- Store secrets securely in GitHub Repository Secrets; never hardcode credentials.
- Use explicit version tags for third-party actions (e.g., `actions/checkout@v4`), never `master` or `latest`.

## 13. Code Review Checklist
> [!IMPORTANT]
> Reviewers must verify:
- [ ] Code follows formatting and typing standards.
- [ ] Edge cases and failure modes are handled gracefully.
- [ ] No hardcoded secrets or credentials exist.
- [ ] New functionality is covered by unit tests.
- [ ] Performance implications of database queries or loops are acceptable.

## 14. Security Checklist
- [ ] Validate and sanitize all external inputs to prevent SQLi/XSS.
- [ ] Enforce Principle of Least Privilege for IAM roles and database users.
- [ ] Use parameterized queries or ORMs exclusively.
- [ ] Ensure all API endpoints implementing sensitive operations enforce authentication (e.g., JWT) and authorization.

## 15. Performance Checklist
- [ ] Implement pagination for all list-returning API endpoints.
- [ ] Utilize caching (e.g., Redis) for frequently accessed, immutable data.
- [ ] Ensure database indexes exist for heavily queried columns.
- [ ] Avoid N+1 query problems in ORM lookups.

## 16. Release Checklist
- [ ] All tests pass on the `main` branch.
- [ ] `CHANGELOG.md` is updated with the new version details.
- [ ] Version numbers are bumped in configuration files (`package.json`, `pyproject.toml`).
- [ ] A formal GitHub Release is drafted and published.

## 17. Dependency Management
- Pin dependency versions explicitly in lockfiles (`package-lock.json`, `poetry.lock`, `requirements.txt`).
- Run dependency vulnerability scans regularly (e.g., Dependabot).
- Limit the introduction of third-party libraries; prefer native standard libraries where viable to reduce supply-chain risk.

## 18. Docker Standards
- Use minimal base images (e.g., `alpine`, `slim`, or `distroless`).
- Never run containers as the `root` user; explicitly create a non-root user in the Dockerfile.
- Leverage multi-stage builds to reduce the final image size.
- Utilize `.dockerignore` to prevent secrets, `.git`, and local environments from entering the build context.

## 19. Environment Variable Standards
- Never commit `.env` files to version control.
- Provide a `.env.example` file containing all required keys with dummy data.
- Validate the presence and type of environment variables at application startup (e.g., using `pydantic-settings`). Fail fast if required variables are missing.

## 20. Logging Standards
- Use structured JSON logging in production environments to enable easy parsing by log aggregators (ELK, Datadog).
- Log Levels:
  - `ERROR`: System failures requiring immediate attention.
  - `WARN`: Expected errors that are handled gracefully.
  - `INFO`: Normal operational events (e.g., startup, shutdown).
  - `DEBUG`: Verbose information for troubleshooting (disabled in production).
- Never log sensitive PII (Passwords, Tokens, Credit Cards).

## 21. API Documentation Standards
- All REST APIs must adhere to the OpenAPI (Swagger) 3.0+ specification.
- Use tools like FastAPI (auto-generated) or Swagger UI to host interactive documentation.
- Every endpoint must document expected request payloads, query parameters, and all possible HTTP response codes (`200`, `400`, `401`, `403`, `404`, `500`).

## 22. Error Handling Standards
- Never expose internal stack traces or database errors to the end-user via API responses.
- Catch specific exceptions rather than broad `Exception` / `Error` classes.
- Return standard HTTP status codes mapping to the error type.
- Wrap application logic in global exception handlers to ensure consistent JSON error responses.

## 23. Monitoring Standards
- Expose a `/health` endpoint for load balancers and orchestrators (e.g., Kubernetes liveness probes).
- Track API metrics: Request Latency, Error Rate, and Throughput (e.g., using Prometheus/Grafana).
- Implement distributed tracing (e.g., OpenTelemetry) for complex microservice or multi-agent orchestrations.
