Below is a **Developer Task Board** that multiple contributors can follow to build the **Cardano Smart Contract Playground IDE** within **March**.

This structure works perfectly for **GitHub Projects, Trello, Jira, or Linear** and breaks the work into **clear issues and milestones** so developers can start coding immediately.

---

# Developer Task Board

## Cardano Smart Contract Playground IDE

This task board organizes the development process into **milestones, epics, and developer tasks**. Each task includes a clear objective so contributors know exactly what to implement.

---

# Table of Contents

1. Project Milestones
2. Development Teams
3. Milestone 1 — Product Definition & UX
4. Milestone 2 — Workspace Standard
5. Milestone 3 — Compiler CLI Runner
6. Milestone 4 — Containerized Build Environment
7. Milestone 5 — Compile API
8. Milestone 6 — Job Orchestration
9. Milestone 7 — Build Caching System
10. Milestone 8 — Security & Sandboxing
11. Milestone 9 — Observability & Metrics
12. Milestone 10 — Frontend IDE Shell
13. Cardano Language Integrations
14. Final Deliverables

---

# 1. Project Milestones

Development is divided into **10 major milestones**.

| Milestone          | Goal                                |
| ------------------ | ----------------------------------- |
| Product Definition | UX flows and compile workflow       |
| Workspace Layout   | Standard project format             |
| Compiler CLI       | Command-line compile tool           |
| Build Environment  | Docker + Nix build system           |
| Compile API        | Backend compilation service         |
| Job Queue          | Manage concurrent builds            |
| Caching System     | Improve compilation speed           |
| Security Sandbox   | Protect the system from abuse       |
| Observability      | Logs, metrics, monitoring           |
| IDE Frontend       | Full Remix-like developer interface |

---

# 2. Development Teams

To accelerate development, contributors should be divided into **specialized teams**.

## Frontend Team

Responsible for:

```
IDE interface
Monaco editor
file explorer
logs panel
compile UI
artifact viewer
```

---

## Backend Team

Responsible for:

```
API development
job orchestration
compile service
authentication
artifact management
```

---

## Compiler Infrastructure Team

Responsible for:

```
language adapters
containerized toolchains
artifact generation
UPLC processing
```

---

## DevOps Team

Responsible for:

```
Docker
Nix environment
build caching
CI/CD pipelines
deployment
```

---

# Milestone 1 — Product Definition & UX Flow

Estimated time: **8 hours**

## Objective

Define how users interact with the playground.

---

## Tasks

### Design IDE Workflow

Create documentation describing the complete workflow:

```
Open template
Edit code
Compile contract
View logs
Download artifacts
```

---

### Define Compile Targets

Document all supported compile targets.

Example targets:

```
Vesting contract
Parameterized Vesting
Marketplace validator
Auction validator
```

Each target must define:

```
build command
entry module
expected outputs
```

---

# Milestone 2 — Playground Workspace Format

Estimated time: **6 hours**

## Objective

Create a standard project layout.

---

## Tasks

### Define Workspace Structure

Example:

```
workspace
│
├── src
│   └── contract.hs
│
├── tests
│
├── fixtures
│
├── plutus.json
│
└── metadata.json
```

---

### Create Example Templates

Templates must include:

```
Vesting contract
Parameterized Vesting contract
```

Templates should include:

```
example datum
example redeemer
example context
```

---

# Milestone 3 — Headless Compiler Runner

Estimated time: **16 hours**

## Objective

Create a CLI command that compiles smart contracts.

---

## CLI Example

```
playground-compile \
  --workspace ./workspace \
  --target vesting
```

---

## Output Artifacts

Compilation must produce:

```
script.cbor
scriptHash
uplc.pretty
uplc.raw
build.log
artifact-manifest.json
```

---

## Artifact Manifest Example

```
{
 "scriptHash": "abc123",
 "sizeBytes": 12345,
 "uplcFile": "contract.uplc",
 "cborFile": "script.cbor"
}
```

---

# Milestone 4 — Containerized Build Environment

Estimated time: **20 hours**

## Objective

Ensure all compilation runs inside containers.

---

## Tasks

### Create Docker Images

Each language must have its own container.

Examples:

```
plutus-worker
aiken-worker
helios-worker
opshin-worker
```

---

### Setup Nix Environment

The Nix environment ensures reproducible builds.

Example components:

```
GHC
Cabal
Plutus libraries
Aiken compiler
Helios runtime
OpShin interpreter
```

---

# Milestone 5 — Compile API

Estimated time: **28 hours**

## Objective

Expose compilation via HTTP API.

---

## API Endpoint

### Submit Compilation Job

```
POST /compile
```

Input:

```
workspace zip
compile target
toolchain version
```

---

## Response Example

```
{
 "jobId": "12345",
 "status": "queued"
}
```

---

## Logs Streaming

Logs must be streamed using:

```
Server Sent Events
or
WebSockets
```

---

# Milestone 6 — Job Orchestration

Estimated time: **20 hours**

## Objective

Manage multiple concurrent builds.

---

## Tasks

Implement job queue.

Recommended stack:

```
Redis
BullMQ
```

---

## Job States

Each job must have a status.

```
queued
running
succeeded
failed
```

---

## Concurrency Limits

Example:

```
Max builds = 5
```

Additional builds must be queued.

---

# Milestone 7 — Build Caching System

Estimated time: **16 hours**

## Objective

Speed up compilation using caching.

---

## Cache Key

Cache key must include:

```
source hash
toolchain version
adapter id
```

---

## Cached Artifacts

Store:

```
compiled scripts
logs
artifact manifests
```

---

# Milestone 8 — Security & Sandboxing

Estimated time: **24 hours**

## Objective

Protect the system from malicious code.

---

## Security Requirements

Compilation jobs must:

```
run as non-root user
have CPU limits
have memory limits
have execution timeout
```

---

## Network Restrictions

Compilation jobs must:

```
disable outbound network
```

---

# Milestone 9 — Observability & Metrics

Estimated time: **12 hours**

## Objective

Provide logs and monitoring.

---

## Metrics to Track

```
compile duration
queue length
cache hit rate
error types
```

---

## Log Retention

Example:

```
retain logs for 7 days
```

---

# Milestone 10 — Frontend IDE Shell

Estimated time: **32 hours**

## Objective

Create a Remix-like IDE interface.

---

## Required Components

### File Explorer

Displays project files.

Example:

```
src/
tests/
fixtures/
```

---

### Monaco Code Editor

Features:

```
syntax highlighting
multi-file editing
language support
```

---

### Bottom Panel

Displays:

```
compile logs
job status
errors
```

---

### Compile Button

Triggers:

```
POST /compile
```

---

# Cardano Language Integrations

The playground must support multiple Cardano languages.

---

## On-chain Languages

These compile to **UPLC (Untyped Plutus Core)**.

Supported languages:

```
Plutus / Plinth
Plutarch
Aiken
Helios
OpShin
Scalus
Pebble
plu-ts
```

Each language must implement a **Language Adapter**.

---

## Contract DSL

Supported DSL:

```
Marlowe
```

Used for:

```
financial contracts
simulation
analysis
```

---

## Off-chain Frameworks

Supported frameworks:

```
Lucid
MeshJS
```

Used for:

```
transaction building
dApp logic
integration testing
```

---

# Final Deliverables

By the end of March the platform must provide:

---

### Remix-like IDE

Includes:

```
file explorer
monaco editor
compile button
logs panel
artifact viewer
```

---

### Smart Contract Compilation

Supports:

```
Plutus
Aiken
Helios
OpShin
```

---

### Compilation Artifacts

Users can download:

```
UPLC scripts
CBOR files
script hash
metadata
```

---

### Simulation Support

Allows developers to:

```
test smart contracts
simulate transactions
analyze execution costs
```

---

### Off-chain Integration

Developers can build transactions using:

```
Lucid
MeshJS
```

---
