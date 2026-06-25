# Python Portfolio with CI/CD

A Flask portfolio website demonstrating **Continuous Integration (CI)** and **Continuous Deployment (CD)** using GitHub Actions YAML workflows.

## Project Structure

```
ci_cd_portfolio/
├── app/                    # Flask application
├── templates/              # HTML templates
├── static/css/             # Stylesheets
├── tests/                  # pytest test suite
├── .github/workflows/
│   ├── ci.yml              # CI pipeline (lint, test, build)
│   └── cd.yml              # CD pipeline (deploy on main)
├── Dockerfile
├── requirements.txt
└── run.py
```

## Run Locally

```bash
python -m venv venv
venv\Scripts\activate        # Windows
pip install -r requirements-dev.txt
python run.py
```

Open [http://localhost:5000](http://localhost:5000)

## CI Pipeline (`ci.yml`)

Triggered on every **push** and **pull request** to `main` or `develop`:

| Job   | Purpose                                      |
|-------|----------------------------------------------|
| Lint  | Ruff lint + format checks                    |
| Test  | pytest with 80% coverage minimum           |
| Build | Validates Docker image builds successfully   |

## CD Pipeline (`cd.yml`)

Triggered on **push to main** (after CI passes):

| Step        | Purpose                                           |
|-------------|---------------------------------------------------|
| Smoke test  | Verifies `/health` endpoint before deploy         |
| Docker push | Builds and pushes image (requires secrets)        |
| Summary     | Writes deployment details to GitHub Actions UI    |

### Docker Hub Secrets (optional)

Add these in **Settings → Secrets and variables → Actions**:

- `DOCKER_USERNAME`
- `DOCKER_PASSWORD`

## Docker

```bash
docker build -t portfolio .
docker run -p 5000:5000 portfolio
```

## Customize

Edit portfolio data in `app/routes.py` (`PORTFOLIO` dict) — name, skills, projects, and links.
