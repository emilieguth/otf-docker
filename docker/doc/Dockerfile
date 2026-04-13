FROM python:3.12-slim

WORKDIR /app

RUN pip install --no-cache-dir mkdocs mkdocs-material

CMD ["mkdocs", "serve", "-a", "0.0.0.0:8000"]
