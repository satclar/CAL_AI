```mermaid
flowchart LR

    %% ---- CLIENTS (4: Consumption) ----
    subgraph Clients["4️⃣ Clients & Channels"]
        Apps["Business & Web Apps"]
        Bots["Bots / Agents"]
        Copilot["Copilot / MCP"]
        PowerApps["Power Platform Apps"]
    end

    %% ---- AI GATEWAY CORE (1: Platform Foundations) ----
    subgraph Gateway["1️⃣ AI Gateway (APIM + Core Access Layer)"]
        APIM["API Management Gateway"]
        Policy["Policies & Governance"]
        Telemetry["Telemetry & Metrics"]
    end

    %% ---- ORCHESTRATION LAYER (2: Composition & Distributed Architecture) ----
    subgraph Orchestration["2️⃣ Orchestration & AI Processing"]
        Router["LLM Router / Orchestrator"]
        Safety["Safety & PII Filters"]
        Cache["Semantic Cache"]
    end

    %% ---- MODELS & TOOLS (2: Part of Capability Composition) ----
    subgraph ModelsTools["2️⃣ Models & Tools"]
        OpenAI["Azure OpenAI / LLMs"]
        OtherLLM["Other LLM Providers"]
        InternalAPIs["Internal APIs / Services"]
        Tools["Domain Tools & Plugins"]
    end

    %% ---- DATA & CONTEXT (2: Composition / Context Enrichment) ----
    subgraph Data["2️⃣ Data & Context Sources"]
        VectorDB["Vector Store / Search"]
        BusinessData["Business Systems / Databases"]
    end

    %% ---- PLATFORM SERVICES (3: Security, Governance, Operations) ----
    subgraph Platform["3️⃣ Platform Services (Security, Governance, Operations)"]
        Identity["Entra ID (Identity)"]
        Observability["Logging & Monitoring"]
        FinOps["Cost & Usage Analytics"]
    end

    %% FLOWS: CLIENTS -> GATEWAY
    Apps --> APIM
    Bots --> APIM
    Copilot --> APIM
    PowerApps --> APIM

    %% GATEWAY FLOWS (1)
    APIM --> Policy
    APIM --> Telemetry
    Policy --> Router

    %% ORCHESTRATION FLOWS (2)
    Router --> Safety
    Router --> Cache

    %% TARGETS (2)
    Router --> OpenAI
    Router --> OtherLLM
    Router --> InternalAPIs
    Router --> Tools
    Router --> VectorDB
    Router --> BusinessData

    %% PLATFORM SERVICES (3)
    APIM --> Identity
    Router --> Identity

    Telemetry --> Observability
    Telemetry --> FinOps


