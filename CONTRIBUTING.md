# Contributing to SecuScan

Thank you for contributing to SecuScan. This project is open to first-time contributors, experienced open source maintainers, and GSSoC participants who want to work on a practical full-stack security platform.

SecuScan is built for learning, defensive security workflows, and ethical testing. Please keep all contributions aligned with authorized, consent-based use.

---

## Before You Start

* Start with a small, reviewable task if this is your first contribution.
* Read `README.md`, `CODE_OF_CONDUCT.md`, and `SECURITY.md` before opening a pull request.
* Read the repository `LICENSE` so you understand how contributions are distributed.
* If you want to work on a larger feature, open or comment on an issue first so effort does not overlap.
* If you are contributing through GSSoC, mention that in the issue or pull request so maintainers can guide scope and review expectations.

---

## Good First Contribution Areas

* Documentation fixes, setup clarification, and onboarding polish
* Frontend UX improvements in `frontend/src`
* Backend validation, test coverage, and API consistency in `backend/secuscan`
* Plugin metadata cleanup and parser improvements in `plugins`
* CI, test reliability, and developer experience

When issue labels are available, look for tags such as:

* `good first issue`
* `documentation`
* `frontend`
* `backend`
* `plugin`
* `help wanted`
* `gssoc`

---

# Local Setup

## Prerequisites

* Python `3.11+`
* Node.js `20+` recommended
* `npm`
* Docker (optional for plugins that depend on containerized tooling)

---

## Recommended Setup

```bash
./setup.sh
./start.sh
```

This starts:

* Backend: `http://127.0.0.1:8000`
* Frontend: `http://127.0.0.1:5173`
* API docs: `http://127.0.0.1:8000/docs`

---

# Manual Setup

## Backend

Python version: `python3` below must resolve to `3.11` or newer.

Check version:

```bash
python3 --version
```

If your system default is older, substitute the full path (e.g. `python3.11`) or use:

```bash
PYTHON=/path/to/python3.11 ./setup.sh
```

### Backend Commands

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r backend/requirements.txt
pip install -r backend/requirements-dev.txt

python3 -m uvicorn backend.secuscan.main:app \
  --reload \
  --host 127.0.0.1 \
  --port 8000
```

---

## Frontend

```bash
cd frontend
npm install
npm run dev -- --host 127.0.0.1 --port 5173
```

---

# Backend Testing Quickstart

This section explains how to run the backend test suite from a fresh checkout without touching the main development environment.

## 1. Prerequisites

Make sure your machine has Python `3.11+`.

```bash
python3 --version
```

If older than `3.11`, use `python3.11` or `python3.12` explicitly.

---

## 2. Run the Full Backend Test Suite

From the repo root:

```bash
./testing/test_python.sh
```

This script automatically:

* Creates isolated environment `venv_tests/`
* Installs dependencies
* Runs all tests in `testing/backend/`

---

## 3. Run a Single Test File

```bash
source venv_tests/bin/activate

python -m pytest testing/backend/unit/test_models.py -v

deactivate
```

Replace `test_models.py` with your desired test file.

Unit tests:

```text
testing/backend/unit/
```

Integration tests:

```text
testing/backend/integration/
```

---

## 4. Requirements Files

| File                           | Purpose               |
| ------------------------------ | --------------------- |
| `backend/requirements.txt`     | Runtime dependencies  |
| `backend/requirements-dev.txt` | Test/dev dependencies |

---

## 5. Common Dependency Issues

### ModuleNotFoundError

Delete `venv_tests/` and rerun:

```bash
./testing/test_python.sh
```

### Wrong Python Version

```bash
python3 --version
```

Use:

```bash
python3.11
```

or

```bash
python3.12
```

### Permission Denied

```bash
chmod +x testing/test_python.sh
```

---

# Project Layout

* `backend/secuscan`

  * FastAPI routes, execution logic, workflows, validation, vault, reporting
* `frontend/src`

  * React pages, scan flows, settings, tests
* `plugins`

  * Plugin metadata, parser code, helpers
* `testing/backend`

  * Backend unit/integration tests
* `frontend/testing`

  * Frontend tests
* `.github`

  * Issue templates, PR templates, CI workflows

---

# Development Workflow

1. Fork repository and create a branch from `main`
2. Pick an issue or open one before large work
3. Keep changes focused
4. Recommended PR size:

   * Under 50 files
   * Under 1,000 lines changed
5. Update tests/docs when behavior changes
6. Open PR with:

   * Clear description
   * Linked issue
   * Screenshots for UI changes

---

## Example Branch Names

```text
docs/improve-contributing-guide
fix/task-status-api
feat/plugin-validation
```

---

# Pull Request Format

Recommended PR titles:

```text
docs: improve contributing guide
fix(api): validate task status input
feat(frontend): add scan empty state
```

Your PR should include:

* Problem description
* Summary of approach
* Linked issues (`Closes #123`)
* Tests run
* Screenshots/recordings for UI
* Docs/migration/environment notes if relevant

---

# Contribution Scoring

## Difficulty Labels

* `level:beginner`
* `level:intermediate`
* `level:advanced`
* `level:critical`

## Quality Labels

* `quality:clean`
* `quality:exceptional`

## Type Bonus Labels

* `type:docs`
* `type:testing`
* `type:accessibility`
* `type:performance`
* `type:security`
* `type:design`
* `type:refactor`
* `type:devops`
* `type:bug`
* `type:feature`

## Validation Labels

* `gssoc:approved`
* `gssoc:invalid`
* `gssoc:spam`
* `gssoc:ai-slop`

Mentor credit:

```text
mentor:username
```

---

# Contributor Points

| Label                 | Points |
| --------------------- | -----: |
| `level:beginner`      | 20 pts |
| `level:intermediate`  | 35 pts |
| `level:advanced`      | 55 pts |
| `level:critical`      | 80 pts |
| `quality:clean`       |   x1.2 |
| `quality:exceptional` |   x1.5 |

Formula:

```text
((difficulty × quality) + type bonus)
```

---

# Mentor Points

| Label                 | Points |
| --------------------- | -----: |
| `level:beginner`      | 10 pts |
| `level:intermediate`  | 20 pts |
| `level:advanced`      | 30 pts |
| `level:critical`      | 50 pts |
| `quality:clean`       |     +5 |
| `quality:exceptional` |    +10 |

Formula:

```text
(base points + quality bonus)
```

---

# Commit Message Conventions

Preferred format:

```text
type(scope): short summary
```

Examples:

```text
feat(frontend): add task result empty state
fix(backend): reject invalid workflow payloads
docs(readme): clarify local setup steps
```

Recommended types:

* `feat`
* `fix`
* `docs`
* `test`
* `refactor`
* `chore`

Guidelines:

* Use imperative mood
* Keep subject under ~72 chars
* Avoid vague messages

---

# Licensing Expectations

By contributing, you agree changes may be distributed under the MIT License.

Avoid:

* Copying incompatible licensed code
* Adding assets without permission checks
* Adding dependencies without license validation

---

# Test Expectations

## Backend Tests

```bash
./testing/test_python.sh
```

## Frontend Unit Tests

```bash
cd frontend
npm run test
```

## Frontend Production Build

```bash
cd frontend
npm run build
```

## Backend API Smoke Tests

```bash
./testing/test_backend.sh
```

## Optional Frontend E2E

```bash
cd frontend
npm run e2e
```

---

# Code Style

## Python

* Follow PEP 8
* Prefer readable code
* Use type hints when useful
* Keep validation close to boundaries

## Frontend

* Use TypeScript + functional React
* Keep logic readable
* Reuse shared UI patterns
* Include accessibility handling

## Tests

* Add/update tests when behavior changes
* Keep fixtures simple

## Docs

* Update contributor docs when setup/workflow changes
* Prefer concrete examples

---

# Review Timeline

Typical expectations:

* Initial review: within 3 business days
* Follow-up review: 2–4 business days

Large/security-sensitive PRs may take longer.

If no response after a week, a polite follow-up is okay.

---

# Review Etiquette

* Be kind and technical
* Focus on code/docs/behavior
* Update same PR when changes requested
* Inactive claimed issues may be reassigned

---

# Need Help?

* Use GitHub issues for bugs/features
* Use PR comments for implementation discussion
* For security reports, follow `SECURITY.md`

---

Thank you for helping make SecuScan more useful, safer, and more welcoming to contributors.

---

# Frontend Generated Artifacts

A lightweight GitHub Action warns if generated folders are committed.

Never commit:

```text
frontend/dist/
frontend/playwright-report/
frontend/test-results/
frontend/.vite/
.vite/deps/
```

If CI fails:

```bash
git rm --cached <file>
echo 'frontend/dist/' >> .gitignore
```
