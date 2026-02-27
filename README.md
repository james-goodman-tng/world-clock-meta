# World Clock - Complete Multi-Repository System

Welcome to the World Clock meta-repository! This repository serves as the central coordination point for the entire World Clock multi-repo system.

## What is This?

This is a **meta-repository** that documents and coordinates all 12 World Clock service repositories.

## All Repositories Now on GitHub!

All 12 service repositories have been published:

### API Services (5)
- https://github.com/james-goodman-tng/api-tokyo
- https://github.com/james-goodman-tng/api-london
- https://github.com/james-goodman-tng/api-newyork
- https://github.com/james-goodman-tng/api-sydney
- https://github.com/james-goodman-tng/api-mumbai

### Frontend Components (6)
- https://github.com/james-goodman-tng/fe-tokyo
- https://github.com/james-goodman-tng/fe-london
- https://github.com/james-goodman-tng/fe-newyork
- https://github.com/james-goodman-tng/fe-sydney
- https://github.com/james-goodman-tng/fe-mumbai
- https://github.com/james-goodman-tng/fe-master (Master Dashboard)

### Orchestration (1)
- https://github.com/james-goodman-tng/clock-orchestration

## System Architecture

```
Browser → Master Dashboard (port 8080)
    ├─ iframe → Tokyo Clock (port 8081) → Tokyo API (port 3001)
    ├─ iframe → London Clock (port 8082) → London API (port 3002)
    ├─ iframe → New York Clock (port 8083) → New York API (port 3003)
    ├─ iframe → Sydney Clock (port 8084) → Sydney API (port 3004)
    └─ iframe → Mumbai Clock (port 8085) → Mumbai API (port 3005)
```

Each city clock is a completely independent microservice with its own:
- Git repository
- API backend
- Frontend UI
- Docker container

## Technology Stack

- **Backend**: Node.js 18 + Express
- **Frontend**: Vanilla HTML/CSS/JavaScript
- **Containers**: Docker + Docker Compose
- **Web Server**: Nginx (for frontends)

## Total Components

**13 repositories:**
- 5 API services
- 6 Frontend components
- 1 Orchestration service
- 1 Meta repository (this one)

## Summary

This project demonstrates:
- ✅ True multi-repository architecture
- ✅ Microservices with complete independence
- ✅ Container-based deployment
- ✅ Production-ready patterns

---

**World Clock Multi-Repository System**