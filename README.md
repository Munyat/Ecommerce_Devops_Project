# E‑Commerce DevOps Microservices Project

> A polyglot microservices e‑commerce app instrumented with OpenTelemetry. Built for demonstrating containerization, orchestration, and observability in a school project.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

## Overview

This repository assembles a production‑style demo of an online store as a distributed system. It is based on the OpenTelemetry Demo and augmented for coursework to showcase:

- Containerized microservices across multiple languages
- Centralized tracing, metrics, and logs with OpenTelemetry
- Local orchestration via Docker Compose (with an Envoy gateway)
- Optional Kubernetes manifests
- Load testing and trace‑based tests

## Architecture (high level)

```
Browser ──► Frontend (Next.js) ──► Frontend Proxy (Envoy)
                                  ├─► Cart (.NET) ──► Valkey (cache)
                                  ├─► Checkout (Go) ──► Kafka ──► Accounting (.NET)/Fraud (Java)
                                  ├─► Product Catalog (Go)
                                  ├─► Recommendation (Python)
                                  ├─► Currency (C++)
                                  ├─► Payment (Node.js)
                                  ├─► Shipping (Go) ──► Quote (PHP)
                                  └─► Email (Ruby)

Telemetry: OpenTelemetry Collector ──► Jaeger, Prometheus, Grafana, OpenSearch
```

## Tech stack

- Languages: TypeScript/Node.js, Go, Python, Java, C#, C++, PHP, Ruby
- Orchestration: Docker Compose; optional Kubernetes
- Gateway: Envoy (`frontend-proxy`)
- Data/infra: PostgreSQL (tests), Valkey (Redis‑compatible), Kafka
- Observability: OpenTelemetry Collector, Jaeger, Prometheus, Grafana, OpenSearch
- Load testing: Locust

## Prerequisites

- Docker (Engine) and Docker Compose
- Make (recommended for helper commands)
- 8 GB+ RAM and 4+ CPU cores recommended

## Quick start (Docker Compose)

The Makefile wires the correct env files and ports.

- Start full demo:
  ```bash
  make start
  ```
- Start minimal demo (lighter resource usage):
  ```bash
  make start-minimal
  ```
- Stop and clean up:
  ```bash
  make stop
  ```

After start, open:

- Demo UI: `http://localhost:8080`
- Jaeger UI: `http://localhost:8080/jaeger/ui`
- Grafana: `http://localhost:8080/grafana/`
- Load Generator UI (Locust): `http://localhost:8080/loadgen/`
- Feature Flag UI: `http://localhost:8080/feature/`

Advanced (direct ports): Prometheus `http://localhost:9090`, Jaeger `16686`, Grafana `3000` (when published).

## Services (selected)

- Frontend (Next.js/TypeScript) – `src/frontend` – port 8080
- Frontend Proxy (Envoy) – `src/frontend-proxy` – port 8080 (gateway)
- Cart (.NET) – `src/cart` – port 7070
- Checkout (Go) – `src/checkout` – port 5050
- Product Catalog (Go) – `src/product-catalog` – port 3550
- Recommendation (Python) – `src/recommendation` – port 9001
- Currency (C++) – `src/currency` – port 7001
- Payment (Node.js) – `src/payment` – port 50051
- Shipping (Go) – `src/shipping` – port 50050
- Quote (PHP) – `src/quote` – port 8090
- Email (Ruby) – `src/email` – port 6060
- Ad (Java) – `src/ad` – port 9555
- Image Provider – `src/image-provider` – port 8081
- Supporting: Kafka, Valkey, Postgres
- Observability: `src/otel-collector`, `src/grafana`, `src/prometheus`, `src/opensearch`

All service ports and addresses are defined in `.env`.

## Common workflows

- Rebuild one service and restart it:
  ```bash
  make redeploy SERVICE=frontend
  ```
- Restart a running service without rebuilding:
  ```bash
  make restart SERVICE=frontend
  ```
- Build all images (honors platform tweaks):
  ```bash
  make build
  ```

## Frontend local development

From repository root, start a dev shell with service ports exposed, then run Next.js dev server inside:
```bash
# open a container with volumes mounted
docker compose run --service-ports \
  -e NODE_ENV=development \
  --volume "$(pwd)/src/frontend:/app" \
  --volume "$(pwd)/pb:/app/pb" \
  --user node \
  --entrypoint sh frontend

# inside the container
npm install
npm run dev
```
The app will be available at `http://localhost:8080`.

## Protobufs

Some services share gRPC/proto definitions stored in `pb/`.
- Regenerate code (inside Docker):
  ```bash
  make docker-generate-protobuf
  ```

## Testing

- Run Cypress (frontend) and trace‑based tests:
  ```bash
  make run-tests
  ```
- Run only trace‑based tests (by service folder name under `test/tracetesting/`):
  ```bash
  make run-tracetesting
  # or a subset
  make run-tracetesting SERVICES_TO_TEST="ad payment"
  ```

## Kubernetes (optional)

- Generate manifests (uses upstream Helm chart):
  ```bash
  make generate-kubernetes-manifests
  ```
- Apply:
  ```bash
  kubectl apply -f kubernetes/
  ```
- Port‑forward the frontend:
  ```bash
  kubectl port-forward svc/frontend 8080:8080
  ```

## Configuration

Most configuration lives in `.env` (and `.env.override` for local overrides). Key values:

- `FRONTEND_PORT=8080` – demo UI port
- `OTEL_COLLECTOR_PORT_GRPC=4317`, `OTEL_COLLECTOR_PORT_HTTP=4318`
- Service addresses like `CART_ADDR`, `CHECKOUT_ADDR`, etc.

ARM64 macOS note: `_JAVA_OPTIONS=-XX:UseSVE=0` is applied from `.env.arm64` automatically by the Makefile when needed.

## Troubleshooting

- Check logs:
  ```bash
  docker compose logs -f <service>
  ```
- Resource pressure: use `make start-minimal`, or allocate more RAM/CPU to Docker
- Port conflicts: stop previous runs with `make stop`, then retry
- Rebuild generated protos if working tree shows untracked generated files:
  ```bash
  make docker-generate-protobuf
  ```

## Attribution

This project is adapted from the OpenTelemetry Demo. See OpenTelemetry docs for guidance on traces, metrics, and logs.

## License

Apache 2.0

## Course information

- Course: DevOps Engineering
- Student: Brian Kipkirui Cheruiyot
- Institution: Nairobi Devops / Strathmore University

— Made for learning DevOps with love and telemetry.