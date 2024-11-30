---
title: Using Docker Image
slug: docker
sidebar_position: 2
---

The simplest way to set up GoiPay is by using the Docker image.

Here you can find an example Docker Compose file:
```yaml title="docker-compose.yml"
version: '3.8'

services:
  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_DB: goipay_db
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres -d goipay_db"]
      interval: 10s
      timeout: 5s
      retries: 5
    ports:
      - "54321:5432"

  migrations:
    image: ghcr.io/kukymbr/goose-docker:3.21.1
    environment:
      - GOOSE_DRIVER=postgres
      - GOOSE_DBSTRING=host=db port=5432 user=postgres password=postgres dbname=goipay_db
    volumes:
      - ./sql/migrations:/migrations
    depends_on:
      db:
        condition: service_healthy

  backend-processor:
    image: chekist32/goipay:latest
    env_file:
      - ./.env
    depends_on:
      migrations:
        condition: service_completed_successfully
    ports:
      - "3000:3000"
```