```mermaid
flowchart LR

    %% ---- CLIENTS (4: Consumption) ----
    subgraph Clients["4️⃣ Clients & Channels (Enterprise Consumption)"]
        Apps["Business & Web Apps"]
        Bots["Bots / Agents"]
        Copilot["Copilot / MCP"]
        PowerApps["Power Platform Apps"]
    end

    %% ---- AI GATEWAY CORE (1: Platform Foundations) ----
    subgraph Gateway["1️⃣ AI Gateway Core (Platform Foundations)"]
        APIM["API Management Gateway"]
        Policy["Policies & Governance"]
        Telemetry["Telemetry & Metrics Pipeline"]
    end

    %% ---- ORCHESTRATION (2: Composition) ----
    subgraph Orchestration["2️⃣ AI Orchestration & Capability Composition"]
        Router["LLM Router / Orchestrator"]
        Safety["Safety & PII Filters"]
        Cache["Semantic Cache"]
    end

    %% ---- MODELS & TOOLS (2) ----
    subgraph ModelsTools["2️⃣ Models, Providers & Tools"]
        OpenAI["Azure OpenAI / LLMs"]
        OtherLLM["Other LLM Providers"]
        InternalAPIs["Internal APIs & Services"]
        Tools["Enterprise Tools & Plugins"]
    end

    %% ---- DATA (2) ----
    subgraph Data["2️⃣ Contextual Data Sources"]
        VectorDB["Vector Store / Semantic Search"]
        BusinessData["Business Systems / Databases"]
    end

    %% ---- PLATFORM SERVICES (3: Governance, Security, Ops) ----
    subgraph Platform["3️⃣ Platform Services (Security, Governance, Operations)"]
        Identity["Entra ID (Identity & Access)"]
        Observability["Logging & Monitoring"]
        FinOps["Cost & Usage Analytics"]
    end

    %% ---- FLOWS ----
    Apps --> APIM
    Bots --> APIM
    Copilot --> APIM
    PowerApps --> APIM

    APIM --> Policy
    APIM --> Telemetry
    Policy --> Router

    Router --> Safety
    Router --> Cache

    Router --> OpenAI
    Router --> OtherLLM
    Router --> InternalAPIs
    Router --> Tools
    Router --> VectorDB
    Router --> BusinessData

    APIM --> Identity
    Router --> Identity

    Telemetry --> Observability
    Telemetry --> FinOps

    %% ---- LEGEND ----
    subgraph Legend["Legend: Section 2 Capability Groups"]
        L1["1️⃣ **Platform Foundations & Core Access Services**  
        (APIM, entry controls, policies, telemetry pipeline)"]

        L2["2️⃣ **Business Capability Composition & Distributed Architecture**  
        (LLM Router, Safety/PII, Semantic Cache, Models, Tools, Data APIs)"]

        L3["3️⃣ **Securing, Operating & Governing Workloads**  
        (Entra ID, Logging, Monitoring, FinOps, Governance Automation)"]

        L4["4️⃣ **Enterprise Consumption & Experience**  
        (Apps, Bots, Power Platform, Copilot/MCP, Unified Consumption Layer)"]
    end



