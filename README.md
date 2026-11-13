# IAntBook — Book API

A Django REST Framework project for browsing books and categories, tracking book views and likes, and downloading book files.

> **Status:** Existing project / development configuration. This repository is **not production-hardened**. Do not deploy the current settings to an internet-facing server without addressing the security notes below.

## Technology

- Python, Django 5.2, Django REST Framework
- SQLite (current checked-in configuration)
- drf-yasg for interactive API documentation
- Pillow for image handling

## Run locally

From the repository root:

```bash
cd book
python -m venv .venv
```

Activate the virtual environment (Windows: `.venv\Scripts\activate`; Linux/macOS: `source .venv/bin/activate`).

```bash
python -m pip install -r req.txt
python manage.py migrate
python manage.py runserver
```

For local development, set a unique `SECRET_KEY` through environment configuration. **Never reuse a development key in production.**

## API routes

All book endpoints are under `/api/`.

| Route | Purpose |
| --- | --- |
| `/api/books/` | List books |
| `/api/books/<id>/` | Book details |
| `/api/category/` | Categories |
| `/api/connection/` | Connections |
| `/api/like/` | Book likes |
| `/api/viewing/` | Book viewing actions |
| `/api/top-books/` | Most-viewed books |
| `/api/books/<id>/download/` | Book download |
| `/admin/` | Django administration |
| `/swagger/`, `/docs/` | Interactive API schema |

Request methods, authentication and response formats depend on the view implementations.

## Security and deployment checklist

The currently committed settings contain development-only defaults: `DEBUG=True`, wildcard `ALLOWED_HOSTS`, permissive CORS and a fallback Django secret. Before production use:

1. Supply a strong unique `SECRET_KEY` through an environment variable and fail startup when missing.
2. Disable debug mode; configure allowed hosts and trusted origins explicitly.
3. Limit CORS to approved client origins and review CSRF settings.
4. Check file download authorization and the Django deployment checklist.
5. Review static/media serving, TLS, dependency versions and automated tests.

No production readiness or successful deployment is claimed by this README.
