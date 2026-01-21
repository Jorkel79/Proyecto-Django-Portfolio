# Proyecto-Django-Portfolio
Proyecto Django sencillo pensado para incluir en un CV / portafolio. Está configurado para usar PostgreSQL y Docker, y trae CI (GitHub Actions) que corre pruebas con Postgres.

Características
- Django app `blog` con CRUD básico de posts.
- PostgreSQL configurado mediante `DATABASE_URL` (dj-database-url).
- Dockerfile + docker-compose (web + db).
- CI con GitHub Actions que levanta Postgres y corre tests.
- .env.example con variables de entorno.
- Licencia: MIT

Requisitos (locally)
- Git
- Docker + Docker Compose (recomendado)
- Python 3.13 (si trabajas local sin Docker)
- VS Code (opcional, ya lo tienes)

Archivos importantes
- Dockerfile
- docker-compose.yml
- .env.example
- project/ (settings, urls, wsgi)
- blog/ (app)
- .github/workflows/ci.yml

Quickstart (Docker — recomendado)
1. Copia `.env.example` a `.env` y ajústalo si quieres:
   cp .env.example .env   # Windows: copy .env.example .env
2. Levanta contenedores:
   docker-compose up --build
3. En una terminal nueva, crea migraciones y superuser (si el contenedor no lo hizo ya):
   docker-compose run web python manage.py migrate
   docker-compose run web python manage.py createsuperuser
4. Abrir en el navegador:
   http://localhost:8000

Ejecutar comandos dentro del contenedor:
- shell: docker-compose run web bash
- migraciones: docker-compose run web python manage.py migrate
- tests: docker-compose run web pytest

Quickstart (sin Docker, local)
1. Crear entorno virtual:
   python -m venv .venv
   source .venv/bin/activate  # Windows: .\.venv\Scripts\activate
2. Instalar dependencias:
   pip install -r requirements.txt
3. Exportar DATABASE_URL (ejemplo):
   export DATABASE_URL=postgres://miuser:mipass@localhost:5432/mi_bd  # Windows PowerShell: $env:DATABASE_URL=...
4. Migrar, crear superuser y correr:
   python manage.py migrate
   python manage.py createsuperuser
   python manage.py runserver

Notas y recomendaciones
- No subas `.env` con credenciales. Usa `.env.example` en el repo y añade valores reales solo en tu máquina o en GitHub Secrets.
- Si pip falla al instalar `psycopg2-binary` en Windows, usa Docker o instala las Build Tools (o WSL).
- Cambia `SECRET_KEY` y `DEBUG=0` en producción.

Licencia: MIT — incluido en el archivo LICENSE.
