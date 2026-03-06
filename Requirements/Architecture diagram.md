# Architecture Diagrams for Plutus Playground Studio

These diagrams illustrate the **core system architecture, services, and workflows** that implement the usability flow specification.

---

# 1. High-Level System Architecture

This diagram shows the **main components of the platform**.

```mermaid
flowchart LR

User[Developer Browser]

User --> IDE[Web IDE Frontend]

IDE --> API[Backend API Gateway]

API --> Auth[Authentication Service]
API --> Project[Project Management Service]
API --> Compile[Compilation Service]
API --> AI[AI Assistant Service]
API --> Deploy[Deployment Service]

Compile --> Worker1[Plutus Compiler Worker]
Compile --> Worker2[Aiken Compiler Worker]
Compile --> Worker3[Helios Compiler Worker]
Compile --> Worker4[OpShin Compiler Worker]

Project --> DB[(PostgreSQL Database)]

Compile --> Artifacts[(Artifact Storage)]

Deploy --> Cardano[Cardano Network]

AI --> Model[AI Model Services]

IDE --> Wallet[Cardano Wallet Integration]
Wallet --> Cardano
```

### Key Insight

The architecture separates:

* **Frontend IDE**
* **API layer**
* **Compiler workers**
* **AI services**
* **Blockchain deployment**

This ensures the platform is **scalable and language-agnostic**.

---

# 2. Frontend IDE Architecture

This diagram explains the **browser development environment**.

```mermaid
flowchart TD

Browser[User Browser]

Browser --> Next[Next.js Application]

Next --> Editor[Monaco Code Editor]
Next --> FileTree[Project File Explorer]
Next --> Terminal[Build Terminal]
Next --> Debugger[Debugger Panel]
Next --> ArtifactViewer[Artifact Viewer]

Next --> WalletUI[Wallet Connector UI]

Next --> APIClient[API Client Layer]

APIClient --> BackendAPI[Backend API]
```

### Responsibilities

Frontend handles:

* project navigation
* editing smart contracts
* running builds
* displaying artifacts
* debugging traces
* wallet interaction

---

# 3. Backend Service Architecture

This diagram explains how **backend services are organized**.

```mermaid
flowchart LR

Gateway[API Gateway]

Gateway --> AuthService
Gateway --> ProjectService
Gateway --> CompileService
Gateway --> TestService
Gateway --> DeployService
Gateway --> AIService

ProjectService --> DB[(PostgreSQL)]

CompileService --> Queue[(Build Queue)]

Queue --> PlutusWorker
Queue --> AikenWorker
Queue --> HeliosWorker
Queue --> OpshinWorker

CompileService --> ArtifactStore[(Artifact Storage)]

DeployService --> CardanoNode[Cardano Node API]

AIService --> LLM[AI Model Engine]
```

### Key Architecture Decision

Compilation is handled by **worker queues** to allow:

* horizontal scaling
* language-specific environments
* containerized builds

---

# 4. Smart Contract Compilation Pipeline

This diagram shows how code becomes **deployable blockchain scripts**.

```mermaid
flowchart LR

EditorCode[Smart Contract Code]

EditorCode --> BuildRequest

BuildRequest --> CompilerService

CompilerService --> Toolchain

Toolchain --> UPLC[Compiled UPLC Script]
Toolchain --> CBOR[CBOR Artifact]
Toolchain --> ScriptHash
Toolchain --> CostAnalysis

UPLC --> ArtifactStorage
CBOR --> ArtifactStorage
ScriptHash --> ArtifactStorage
CostAnalysis --> ArtifactStorage

ArtifactStorage --> IDEArtifacts[Artifact Viewer]
```

---

# 5. Smart Contract Testing Architecture

```mermaid
flowchart TD

Developer[Test Developer]

Developer --> WriteTests

WriteTests --> TestRunner

TestRunner --> Simulator[Blockchain Simulator]

Simulator --> ExecuteTx[Execute Transactions]

ExecuteTx --> Results[Test Results]

Results --> IDEPanel[Test Dashboard]
```

Testing supports:

* unit tests
* simulation
* integration tests
* property tests

---

# 6. On-Chain / Off-Chain Integration Architecture

```mermaid
flowchart LR

OnChain[Smart Contract Code]

OffChain[Off-chain Application]

OnChain --> Script

Script --> TransactionBuilder

OffChain --> TransactionBuilder

TransactionBuilder --> Wallet

Wallet --> SubmitTx

SubmitTx --> CardanoNetwork
```

This layer connects:

* **smart contracts**
* **wallet interactions**
* **transaction building**

---

# 7. Deployment Architecture

```mermaid
flowchart LR

ProjectCode --> BuildArtifacts

BuildArtifacts --> DeploymentService

DeploymentService --> FrontendHosting
DeploymentService --> BackendHosting
DeploymentService --> CardanoDeployment

FrontendHosting --> WebApp

BackendHosting --> APIService

CardanoDeployment --> Blockchain
```

This enables **WordPress-style deployment for dApps**.

---

# 8. AI Assisted Development Architecture

```mermaid
flowchart TD

Developer --> AIRequest

AIRequest --> AIGateway

AIGateway --> CodeGen
AIGateway --> DebugAssist
AIGateway --> Optimization
AIGateway --> Documentation

CodeGen --> IDEEditor
DebugAssist --> IDEDebugger
Optimization --> CompilerHints
Documentation --> IDEDocs
```

---

# 9. Project Storage Architecture

```mermaid
flowchart LR

UserProject --> FileStorage

FileStorage --> Contracts
FileStorage --> Tests
FileStorage --> Offchain
FileStorage --> Frontend
FileStorage --> Config

FileStorage --> DB[(PostgreSQL)]

DB --> Projects
DB --> Users
DB --> Artifacts
DB --> DeploymentLogs
```

---

# 10. Developer Workflow Diagram

This diagram matches your **Usability Flow Specification**.

```mermaid
flowchart TD

Start --> SelectLanguage

SelectLanguage --> CreateProject

CreateProject --> WriteCode

WriteCode --> Compile

Compile --> Debug

Debug --> WriteTests

WriteTests --> GenerateOffChain

GenerateOffChain --> BuildFrontend

BuildFrontend --> IntegrateApp

IntegrateApp --> Deploy

Deploy --> ExportCode

ExportCode --> End
```

---
