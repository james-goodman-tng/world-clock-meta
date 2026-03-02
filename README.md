# World Clock - Complete Multi-Repository System

Welcome to the World Clock meta-repository! This repository coordinates all 12 World Clock service repositories using git submodules.

## What is This?

This is a **meta-repository** that uses git submodules to reference all 12 World Clock service repositories. It provides:
- Single-command cloning of all services
- Version coordination across services
- Complete system documentation
- Release management capabilities

## Quick Start

### Clone with All Submodules

```bash
# Clone this repo with all 12 service repositories
git clone --recurse-submodules https://github.com/james-goodman-tng/world-clock-meta.git
cd world-clock-meta

# Start all services
cd clock-orchestration
./start-all.sh

# Open the dashboard
open http://localhost:8080
```

That's it! You now have all 12 services running.

### Alternative: Initialize Submodules After Cloning

If you already cloned without `--recurse-submodules`:

```bash
git clone https://github.com/james-goodman-tng/world-clock-meta.git
cd world-clock-meta
git submodule init
git submodule update
```

## All Repositories on GitHub

All 12 service repositories are publicly available:

### API Services (5)
- **api-tokyo**: https://github.com/james-goodman-tng/api-tokyo
- **api-london**: https://github.com/james-goodman-tng/api-london
- **api-newyork**: https://github.com/james-goodman-tng/api-newyork
- **api-sydney**: https://github.com/james-goodman-tng/api-sydney
- **api-mumbai**: https://github.com/james-goodman-tng/api-mumbai

### Frontend Components (6)
- **fe-tokyo**: https://github.com/james-goodman-tng/fe-tokyo
- **fe-london**: https://github.com/james-goodman-tng/fe-london
- **fe-newyork**: https://github.com/james-goodman-tng/fe-newyork
- **fe-sydney**: https://github.com/james-goodman-tng/fe-sydney
- **fe-mumbai**: https://github.com/james-goodman-tng/fe-mumbai
- **fe-master**: https://github.com/james-goodman-tng/fe-master (Master Dashboard)

### Orchestration (1)
- **clock-orchestration**: https://github.com/james-goodman-tng/clock-orchestration

### Meta Repository (1)
- **world-clock-meta**: https://github.com/james-goodman-tng/world-clock-meta (this repo)

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

## Understanding Git Submodules

This meta-repository uses git submodules to reference specific commits of each service repository. When you clone with `--recurse-submodules`, git automatically:
1. Clones the meta repository
2. Initializes all 12 submodules
3. Checks out the specific commit referenced by the meta repo

### Benefits

✅ **One-command clone** - Get all 12 repos at once
✅ **Version coordination** - Track specific versions that work together
✅ **Release management** - Tag combinations of versions
✅ **Reproducible builds** - Everyone gets same versions
✅ **Easy rollback** - Checkout old tag to get old versions

## Common Tasks

### Update All Submodules to Latest

```bash
git submodule update --remote --merge
git add .
git commit -m "Update all submodules to latest"
git push
```

### Check Submodule Status

```bash
git submodule status
```

### Start the System

```bash
cd clock-orchestration
./start-all.sh
```

### Check if Services are Running

```bash
cd clock-orchestration
./check-services.sh
```

### Stop the System

```bash
cd clock-orchestration
./stop-all.sh
```

### Work on a Specific Service

```bash
cd api-tokyo
# Make changes
vim index.js
git add .
git commit -m "Update time format"
git push

# Update meta-repo reference
cd ..
git add api-tokyo
git commit -m "api-tokyo: Update time format"
git push
```

## Alternative Setup Methods

### Option 1: Use This Meta Repository (Recommended)

Best for: Managing all services together, version coordination, releases

```bash
git clone --recurse-submodules https://github.com/james-goodman-tng/world-clock-meta.git
cd world-clock-meta/clock-orchestration
./start-all.sh
```

### Option 2: Clone Individual Repos

Best for: Working on specific services, independent development

```bash
# Use the clone script from clock-orchestration
mkdir world-clock && cd world-clock
bash <(curl -s https://raw.githubusercontent.com/james-goodman-tng/clock-orchestration/main/clone-all-repos.sh)
cd clock-orchestration
./start-all.sh
```

### Option 3: Manual Clone

Best for: Custom setups, specific service combinations

```bash
mkdir world-clock && cd world-clock
git clone https://github.com/james-goodman-tng/api-tokyo.git
git clone https://github.com/james-goodman-tng/api-london.git
# ... clone other repos
cd clock-orchestration
./start-all.sh
```

## Release Management

### Creating a Release

```bash
# Test that all services work together
cd clock-orchestration
./start-all.sh
./check-services.sh

# If all good, tag the meta repo
cd ..
git tag -a v1.0.0 -m "Release 1.0.0: All services tested and stable"
git push --tags
```

### Deploying a Specific Release

```bash
git clone --recurse-submodules https://github.com/james-goodman-tng/world-clock-meta.git
cd world-clock-meta
git checkout v1.0.0
git submodule update --init --recursive
cd clock-orchestration
./start-all.sh
```

## Technology Stack

- **Backend**: Node.js 18 + Express
- **Frontend**: Vanilla HTML/CSS/JavaScript
- **Containers**: Docker + Docker Compose
- **Web Server**: Nginx (for frontends)
- **Version Control**: Git + Git Submodules

## Prerequisites

- Docker Desktop installed
- Git installed
- Bash shell (Mac/Linux/WSL)
- Ports 3001-3005 and 8080-8085 available

## Troubleshooting

### Submodules are empty

```bash
git submodule init
git submodule update
```

### Services won't start

```bash
cd clock-orchestration
docker-compose ps
docker-compose logs
```

### Want to reset everything

```bash
git submodule update --init --recursive --force
cd clock-orchestration
./stop-all.sh
./start-all.sh
```

### Submodule detached HEAD

This is normal! Submodules are checked out at specific commits. To work on a submodule:

```bash
cd api-tokyo
git checkout main
git pull
# Make changes, commit, push
cd ..
git add api-tokyo
git commit -m "Update api-tokyo reference"
```

## Directory Structure

After cloning with submodules:

```
world-clock-meta/                    (This repository)
├── README.md                        (You are here)
├── .gitmodules                      (Submodule configuration)
├── .gitignore                       (Git ignore rules)
│
└── [Submodules - all 12 service repos]
    ├── api-tokyo/
    ├── api-london/
    ├── api-newyork/
    ├── api-sydney/
    ├── api-mumbai/
    ├── fe-tokyo/
    ├── fe-london/
    ├── fe-newyork/
    ├── fe-sydney/
    ├── fe-mumbai/
    ├── fe-master/
    └── clock-orchestration/
```

## Repository Organization

This is **Repository #13** in the World Clock system:
- Repositories 1-12: Individual service repositories
- Repository 13: This meta-repository (coordinates all)

The meta-repository doesn't replace the individual repos - it **coordinates** them using git submodules.

## Contributing

Each service repository is independent:
1. Navigate to the service: `cd api-tokyo`
2. Create a branch: `git checkout -b feature-x`
3. Make changes and commit
4. Push: `git push origin feature-x`
5. Update meta-repo: `cd .. && git add api-tokyo`

## Resources

- **Orchestration Repository**: https://github.com/james-goodman-tng/clock-orchestration
- **Clone All Script**: See clock-orchestration/clone-all-repos.sh
- **Organization**: https://github.com/james-goodman-tng

## Summary

This meta-repository is your **single source of truth** for the World Clock system. It:

✅ References all 12 service repositories as submodules
✅ Enables one-command cloning of entire system
✅ Coordinates versions and releases
✅ Provides reproducible builds
✅ Supports easy rollback via tags

**Total Components**: 13 repositories (12 services + 1 meta)

**Get Started**: 
```bash
git clone --recurse-submodules https://github.com/james-goodman-tng/world-clock-meta.git
cd world-clock-meta/clock-orchestration
./start-all.sh
```

Then open http://localhost:8080 and watch the clocks tick!

---

**World Clock Multi-Repository System** - Demonstrating enterprise-grade microservices architecture with complete service independence and git submodule coordination.
