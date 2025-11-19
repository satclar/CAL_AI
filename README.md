```mermaid
flowchart LR

    %% ---- CLIENTS ----
    subgraph Clients["Clients & Channels"]
        Apps["Business & Web Apps"]
        Bots["Bots / Agents"]
        Copilot["Copilot / MCP"]
        PowerApps["Power Platform Apps"]
    end

    %% ---- AI GATEWAY CORE ----
    subgraph Gateway["AI Gateway (APIM + Orchestration)"]
        APIM["API Management Gateway"]
        Policy["Policies & Governance"]
        Safety["Safety & PII Filters"]
        Router["LLM Router / Orchestrator"]
        Cache["Semantic Cache"]
        Telemetry["Telemetry & Metrics"]
    end

    %% ---- MODELS & TOOLS ----
    subgraph ModelsTools["Models & Tools"]
        OpenAI["Azure OpenAI / LLMs"]
        OtherLLM["Other LLM Providers"]
        InternalAPIs["Internal APIs / Services"]
        Tools["Domain Tools & Plugins"]
    end

    %% ---- DATA & CONTEXT ----
    subgraph Data["Data & Context"]
        VectorDB["Vector Store / Search"]
        BusinessData["Business Systems / Databases"]
    end

    %% ---- PLATFORM SERVICES ----
    subgraph Platform["Platform Services"]
        Identity["Entra ID (Identity)"]
        Observability["Logging & Monitoring"]
        FinOps["Cost & Usage Analytics"]
    end

    %% FLOWS: CLIENTS -> GATEWAY
    Apps --> APIM
    Bots --> APIM
    Copilot --> APIM
    PowerApps --> APIM

    %% INSIDE GATEWAY
    APIM --> Policy
    Policy --> Router
    Router --> Safety
    Router --> Cache
    APIM --> Telemetry
    Router --> Telemetry

    %% GATEWAY -> MODELS / TOOLS / DATA
    Router --> OpenAI
    Router --> OtherLLM
    Router --> InternalAPIs
    Router --> Tools
    Router --> VectorDB
    Router --> BusinessData

    %% PLATFORM SERVICES
    APIM --> Identity
    Router --> Identity

    Telemetry --> Observability
    Telemetry --> FinOps

