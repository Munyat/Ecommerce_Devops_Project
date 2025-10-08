# E-Commerce DevOps Project 🛒

> **DevOps School Project** - Demonstrating modern DevOps practices with a microservices-based e-commerce application

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-Enabled-2496ED?logo=docker)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-Ready-326CE5?logo=kubernetes)](https://kubernetes.io/)

## 📋 Table of Contents

- [Overview](#overview)
- [Project Objectives](#project-objectives)
- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Deployment Options](#deployment-options)
- [DevOps Practices Implemented](#devops-practices-implemented)
- [Monitoring & Observability](#monitoring--observability)
- [Learning Outcomes](#learning-outcomes)
- [Troubleshooting](#troubleshooting)
- [Acknowledgments](#acknowledgments)

## 🎯 Overview

This project is a **DevOps-focused implementation** of a microservices-based e-commerce application, forked from the [OpenTelemetry Demo](https://github.com/open-telemetry/opentelemetry-demo). It serves as a comprehensive demonstration of modern DevOps principles, containerization, orchestration, and observability practices.

The application simulates a real-world online astronomy shop with multiple interconnected services, providing an ideal environment to practice and showcase DevOps skills.

## 🎓 Project Objectives

This school project demonstrates the following DevOps competencies:

1. **Containerization**: Dockerizing microservices for consistent deployment
2. **Orchestration**: Managing multi-container applications with Docker Compose/Kubernetes
3. **CI/CD**: Implementing continuous integration and deployment pipelines
4. **Monitoring**: Setting up comprehensive observability with OpenTelemetry
5. **Infrastructure as Code**: Managing infrastructure through declarative configuration
6. **Microservices Architecture**: Understanding distributed system design and communication

## 🏗️ Architecture

The application consists of multiple microservices written in different programming languages, demonstrating polyglot architecture:

```
┌─────────────────────────────────────────────────────────────┐
│                        Frontend (Next.js)                    │
└────────────────────┬────────────────────────────────────────┘
                     │
     ┌───────────────┼───────────────────────┐
     │               │                       │
┌────▼────┐   ┌─────▼──────┐   ┌───────────▼────────┐
│ Cart    │   │ Checkout   │   │ Product Catalog    │
│ Service │   │ Service    │   │ Service            │
└─────────┘   └────────────┘   └────────────────────┘
     │               │                       │
     └───────────────┼───────────────────────┘
                     │
            ┌────────▼────────┐
            │  Payment Service │
            └─────────────────┘
```

### Microservices Components:

- **Frontend**: Web UI for customers (Next.js/React)
- **Cart Service**: Shopping cart functionality
- **Product Catalog Service**: Product inventory and details
- **Checkout Service**: Order processing
- **Payment Service**: Payment processing simulation
- **Recommendation Service**: Product recommendations
- **Ad Service**: Advertisement management
- **Email Service**: Email notifications
- **Shipping Service**: Shipping calculations
- **Currency Service**: Currency conversion

## 🛠️ Technologies Used

### Core Technologies:
- **Languages**: Go, Java, Python, Node.js, .NET, PHP, Ruby
- **Container Runtime**: Docker
- **Orchestration**: Docker Compose, Kubernetes
- **Observability**: OpenTelemetry, Jaeger, Prometheus, Grafana
- **Service Mesh**: Optional (Istio/Linkerd)
- **Databases**: Redis (cache), PostgreSQL

### DevOps Tools:
- **Version Control**: Git, GitHub
- **CI/CD**: GitHub Actions (configurable)
- **Infrastructure as Code**: Docker Compose files, Kubernetes manifests
- **Monitoring**: OpenTelemetry Collector, Prometheus
- **Logging**: Fluent Bit, OpenTelemetry

## 📦 Prerequisites

Before running this project, ensure you have the following installed:

- **Docker Desktop** (v20.10+) or Docker Engine with Docker Compose
- **Git** for version control
- **kubectl** (for Kubernetes deployment)
- **Helm** (optional, for Kubernetes deployment)
- Minimum **6GB RAM** allocated to Docker
- Minimum **4 CPU cores** recommended

### System Requirements:
```
Minimum:
- RAM: 6GB
- CPU: 4 cores
- Disk: 20GB free space

Recommended:
- RAM: 8GB+
- CPU: 6+ cores
- Disk: 30GB+ free space
```

## 🚀 Quick Start

### Option 1: Docker Compose (Recommended for Development)

1. **Clone the repository**
   ```bash
   git clone https://github.com/Munyat/Ecommerce_Devops_Project.git
   cd Ecommerce_Devops_Project
   ```

2. **Start the application**
   ```bash
   docker compose up -d
   ```

3. **Access the application**
   - Frontend: http://localhost:8080
   - Jaeger UI: http://localhost:16686
   - Grafana: http://localhost:3000
   - Prometheus: http://localhost:9090

4. **Stop the application**
   ```bash
   docker compose down
   ```

### Option 2: Kubernetes

1. **Apply Kubernetes manifests**
   ```bash
   kubectl apply -f kubernetes/
   ```

2. **Verify deployment**
   ```bash
   kubectl get pods
   kubectl get services
   ```

3. **Access via port-forward**
   ```bash
   kubectl port-forward svc/frontend 8080:8080
   ```

## 🌐 Deployment Options

### Local Development
- Docker Compose for rapid iteration
- Hot-reload enabled for frontend services

### Production-like Environment
- Kubernetes cluster (minikube, kind, or cloud providers)
- Helm charts for streamlined deployment
- Ingress controllers for routing

### Cloud Deployment
- AWS EKS, Google GKE, or Azure AKS
- Cloud-native monitoring integration
- Auto-scaling configurations

## 🔧 DevOps Practices Implemented

### 1. Containerization
- Each microservice runs in its own Docker container
- Multi-stage builds for optimized image sizes
- Health checks for container reliability

### 2. Infrastructure as Code
- Declarative configuration with Docker Compose
- Kubernetes manifests for production deployment
- Version-controlled infrastructure

### 3. Observability
- **Distributed Tracing**: Full request tracing across services
- **Metrics Collection**: Performance and business metrics
- **Logging**: Centralized log aggregation
- **Dashboards**: Pre-configured Grafana dashboards

### 4. Service Communication
- REST APIs for synchronous communication
- gRPC for high-performance inter-service calls
- Message queues for asynchronous operations

### 5. Security Best Practices
- Non-root containers
- Minimal base images
- Network policies (Kubernetes)
- Secret management

## 📊 Monitoring & Observability

### OpenTelemetry Integration
This project showcases complete OpenTelemetry instrumentation:

- **Traces**: End-to-end request tracing
- **Metrics**: Performance metrics collection
- **Logs**: Structured logging across services

### Accessing Monitoring Tools

| Tool | URL | Purpose |
|------|-----|---------|
| Jaeger | http://localhost:16686 | Distributed tracing |
| Grafana | http://localhost:3000 | Metrics visualization |
| Prometheus | http://localhost:9090 | Metrics storage & querying |

### Key Metrics to Monitor
- Request latency across services
- Error rates and HTTP status codes
- Service dependencies and call graphs
- Database query performance
- Cache hit/miss ratios

## 📚 Learning Outcomes

By working on this project, I gained hands-on experience with:

1. **Microservices Architecture**
   - Understanding service decomposition
   - Inter-service communication patterns
   - Handling distributed transactions

2. **Containerization**
   - Writing production-ready Dockerfiles
   - Optimizing container images
   - Managing container lifecycles

3. **Orchestration**
   - Deploying multi-container applications
   - Service discovery and load balancing
   - Scaling strategies

4. **Observability**
   - Implementing distributed tracing
   - Collecting and visualizing metrics
   - Debugging distributed systems

5. **DevOps Workflows**
   - CI/CD pipeline design
   - Automated testing strategies
   - Deployment automation

## 🐛 Troubleshooting

### Common Issues

**Services not starting**
```bash
# Check container logs
docker compose logs [service-name]

# Verify resource allocation
docker stats
```

**Port conflicts**
```bash
# Check if ports are in use
lsof -i :<port-number>

# Modify port mappings in docker-compose.yml
```

**Out of memory errors**
```bash
# Increase Docker memory allocation in Docker Desktop settings
# Or scale down services for development:
docker compose up -d frontend cartservice productcatalogservice
```

**Image pull errors**
```bash
# Pull images explicitly
docker compose pull

# Build images locally
docker compose build
```

## 📖 Additional Resources

- [OpenTelemetry Documentation](https://opentelemetry.io/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Microservices Patterns](https://microservices.io/patterns/)


## 📄 License

This project inherits the Apache 2.0 License.

---

## 🎓 Project Information

**Course**: DevOps Engineering  
**Student**: Brian Kipkirui Cheruiyot
**Institution**: Nairobi Devops/Strathmore university

### Project Focus Areas
- ✅ Containerization with Docker
- ✅ Container orchestration
- ✅ Microservices architecture
- ✅ Observability and monitoring
- ✅ Infrastructure as Code
- ✅ CI/CD pipeline implementation

---

**Made with ❤️ for learning DevOps**
