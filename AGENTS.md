# AGENTS.md

Contexto del proyecto para los agentes de IA. Léalo antes de cualquier cambio.

## Proyecto

Plataforma web lúdica de cursos para niños. Curso: Geografía de Colombia - Niveles (ver `app/proyecto.py`).
Roles: docente y niño. El niño entra con código de clase y avatar, sin correo.

## Stack

- Python 3.11+, FastAPI, plantillas Jinja2, SQLModel
- pytest con TestClient; Ruff (line-length 100, reglas E/F/B/I)
- CI en GitHub Actions (`.github/workflows/ci.yml`); despliegue en Render (`render.yaml`)

## Comandos

- Instalar: `python -m venv .venv` → `.venv\Scripts\activate` → `pip install -r requirements-dev.txt` (Windows); `source .venv/bin/activate` (Linux/macOS)
- Ejecutar (dev): `uvicorn app.main:app --reload` (http://127.0.0.1:8000, docs en /docs)
- Ejecutar (Render/prod): `uvicorn app.main:app --host 0.0.0.0 --port $PORT`
- Pruebas: `pytest -v` (testpaths: `tests`, pythonpath: `.`)
- Un solo test: `pytest tests/test_inicio.py -v` o `pytest -k <nombre>`
- Estilo: `ruff check .`
- Pre-commit: `pre-commit install` (ejecuta ruff + pytest en cada commit)

## Arquitectura y entrypoints

- `app/main.py`: crea la FastAPI, monta `/static`, incluye routers `paginas` y `api`
- `app/rutas/paginas.py`: páginas HTML (Jinja2) y service worker `/sw.js`
- `app/rutas/api.py`: endpoints `/salud` y `/api/proyecto` (documentados en /docs)
- `app/proyecto.py`: APRENDIZ, CURSO, MECANICA, VERSION, URL_PUBLICA — edite aquí los datos del proyecto; lo leen la página, la API y `entregar.py`
- `app/modelos/`: solo `__init__.py` aún; tablas SQLModel por definir (SQLite en dev, PostgreSQL en Render)
- `tests/`: pruebas unitarias; `tests/aceptacion/`: vacío, pruebas de aceptación (semana 3), nombre `test_<historia>.py`
- `specs/`: spec.md, plan.md, tasks.md, user-flow.md, adr/

## Entorno y secretos

- Copie `.env.example` a `.env` y defina SECRET_KEY (`python -c "import secrets; print(secrets.token_urlsafe(32))"`) y DATABASE_URL
- `.env` y `*.db` están en `.gitignore`: nunca subir secretos ni bases de datos locales
- `entregas/*.pdf` no se sube al repositorio

## Flujo

- Cambios pequeños, una tarea por rama, prueba antes del código
- Verificar: `ruff check .` y `pytest -v`
- Despliegue: Render vía `render.yaml`, health check `/salud`, build con `requirements.txt` (no dev)

## Que no hacer
- No hacer commit ni push: los hace el desarrollador.

## Convenciones
- Al iniciar cada sesión, leer STATE.md.

## Lecciones aprendidas
