# Flask on Docker

Flask + Postgres + Gunicorn + Nginx. Dev: Flask dev server; Prod: Gunicorn + Nginx, static/media via Nginx.

## Dev
- `docker-compose up -d --build`
- `docker-compose exec web python manage.py create_db`
- `docker-compose exec web python manage.py seed_db`
- http://localhost:5002

## Prod
- `docker-compose -f docker-compose.prod.yml up -d --build`
- `docker-compose -f docker-compose.prod.yml exec web python manage.py create_db`
- http://localhost:1433

## Env
- `.env.dev`, `.env.prod`, `.env.prod.db`

## Structure
- `services/web`: Flask app, Dockerfiles, entrypoints.
- `services/nginx`: Nginx config.
- `docker-compose.yml`, `docker-compose.prod.yml`

## Notes
- Prod uses multi-stage build, non-root user.
- Entrypoint waits for Postgres; dev runs `create_db`.
- Static/media: shared volumes, Nginx aliases `/static/`, `/media/`.
