```mermaid
flowchart LR

    %% ---------- CLASS DEFINITIONS (COLORS) ----------
    classDef client      fill:#E3F2FD,stroke:#1E88E5,stroke-width:1px,color:#0D47A1;
    classDef edge        fill:#FFF3E0,stroke:#FB8C00,stroke-width:1px,color:#E65100;
    classDef access      fill:#E8F5E9,stroke:#43A047,stroke-width:1px,color:#1B5E20;
    classDef orchestration fill:#F3E5F5,stroke:#8E24AA,stroke-width:1px,color:#4A148C;
    classDef identity    fill:#FCE4EC,stroke:#D81B60,stroke-width:1px,color:#880E4F;
    classDef backend     fill:#E0F7FA,stroke:#00838F,stroke-width:1px,color:#006064;
    classDef observability fill:#FFFDE7,stroke:#FDD835,stroke-width:1px,color:#F9A825;
    classDef integration fill:#ECEFF1,stroke:#546E7A,stroke-width:1px,color:#263238;
    classDef legend      fill:#FFFFFF,stroke:#B0BEC5,stroke-width:1px,color:#37474F,font-size:11px;

    %% ---------- CLIENTS ----------
    subgraph Clients["Clients & Consumers"]
        AppUser["Business Apps"]
        Bots["Enterprise Bots/Agents"]
        Copilot["Copilot / MCP"]
        PowerUsers["Power Platform Apps"]
    end

    %% ---------- EDGE ----------
    subgraph Edge["Edge & Perimeter"]
        AFD["Azure Front Door + WAF"]
    end

    %% ---------- ACCESS LAYER ----------
    subgraph Access["Enterprise Access Layer (API + AI Gateway)"]
        APIM["Azure API Management"]
        DevPortal["Developer Portal & API Center"]
    end

    %% ---------- ORCHESTRATION ----------
    subgraph Orchestration["AI Gateway Orchestration"]
        Router["LLM Router Service"]
        Safety["Safety & PII Pipeline"]
        Schemas["Schema & Contract Layer"]
    end

    %% ---------- IDENTITY ----------
    subgraph Identity["Identity & Security"]
        Entra["Entra ID"]
        KeyVault["Azure Key Vault"]
    end

    %% ---------- BACKENDS ----------
    subgraph Backends["AI + Application Backends"]
        OpenAI["Azure OpenAI / LLMs"]
        VecSearch["Azure AI Search (Vector)"]
        Apps["Backend APIs"]
        Events["Event Grid / Service Bus (DLQ)"]
    end

    %% ---------- OBSERVABILITY ----------
    subgraph Observability["Observability & FinOps"]
        Logs["App Insights / Log Analytics"]
        FinOps["FinOps Dashboards"]
        PolicyGov["Policy Governance Engine"]
    end

    %% ---------- INTEGRATIONS ----------
    subgraph Integrations["Enterprise Integrations"]
        PwrPlat["Power Platform Connectors"]
        MCPNode["MCP Servers / Plugins"]
        Monet["Monetization & Subscription Plans"]
    end

    %% ---------- LEGEND ----------
    subgraph Legend["Legend: Azure Components & Key Capabilities"]
        L_APIM["APIM (green): gateway, products, policies, quotas, versioning, schema validation"]
        L_AFD["Front Door/WAF (orange): edge routing, SSL offload, threat protection"]
        L_Entra["Entra ID (pink): OAuth2/OIDC, RBAC/ABAC, OBO flows"]
        L_KeyVault["Key Vault (pink): secrets storage, key rotation, identity-based access"]
        L_OpenAI["Azure OpenAI (teal): LLMs, embeddings, chat/completions"]
        L_AI_Search["AI Search (teal): vector store, semantic caching, retrieval"]
        L_Apps["Backend APIs (teal): domain logic, business capabilities"]
        L_Events["Event Grid/Service Bus (teal): async messaging, DLQ for failed calls"]
        L_Logs["App Insights/Log Analytics (yellow): metrics, traces, SLA/SLO, anomaly detection"]
        L_FinOps["FinOps Dashboards (yellow): token & cost analytics, budgets, alerts"]
        L_APICenter["Dev Portal/API Center (green): catalog, discovery, onboarding, docs"]
        L_PowerPlat["Power Platform (gray): low-code apps using APIM connectors"]
        L_MCP["MCP / Copilot (gray): plugin integration with enterprise APIs"]
    end

    %% ---------- FLOWS ----------
    AppUser --> AFD
    Bots --> AFD
    Copilot --> AFD
    PowerUsers --> AFD

    AFD --> APIM

    APIM --> Router
    APIM --> Apps

    Router --> Safety
    Router --> Schemas
    Router --> OpenAI
    Router --> VecSearch
    Router --> Events

    APIM --> DevPortal
    DevPortal --> AppUser

    APIM --> PwrPlat
    APIM --> MCPNode
    APIM --> Monet
    MCPNode --> Copilot

    AppUser -. auth tokens .-> Entra
    APIM --> Entra
    Router --> Entra

    APIM --> KeyVault
    Router --> KeyVault

    APIM --> Logs
    Router --> Logs
    Apps --> Logs
    OpenAI --> Logs

    Logs --> FinOps
    Logs --> PolicyGov
    PolicyGov --> APIM
    PolicyGov --> Router

    %% ---------- CLASS ASSIGNMENTS ----------
    class AppUser,Bots,Copilot,PowerUsers client;
    class AFD edge;
    class APIM,DevPortal access;
    class Router,Safety,Schemas orchestration;
    class Entra,KeyVault identity;
    class OpenAI,VecSearch,Apps,Events backend;
    class Logs,FinOps,PolicyGov observability;
    class PwrPlat,MCPNode,Monet integration;
    class L_APIM,L_APICenter access,legend;
    class L_AFD edge,legend;
    class L_Entra,L_KeyVault identity,legend;
    class L_OpenAI,L_AI_Search,L_Apps,L_Events backend,legend;
    class L_Logs,L_FinOps observability,legend;
    class L_PowerPlat,L_MCP integration,legend;
