# System Architecture - 5G Network Framework

High-level architecture of the academic 5G network framework project.  
Shows components, flows, use cases, slices, and automated verification.

---

```mermaid
flowchart TB
    %% User Interface
    UI[UI - Web GUI]

    %% Use Cases
    subgraph UseCases["Use Case Selection"]
        UC1[Industrial IoT]
        UC2[Connected Cars]
        UC3[Smart City]
    end

    %% Controller / Backend
    Controller[Controller Backend]

    %% Configuration Module
    Config[Configuration Module - Use Cases & Slices]

    %% Network Components
    subgraph Network["5G Network Components"]
        subgraph RAN_Sub["RAN"]
            gNB[gNodeB gNB]
            UE[UE Simulator optional]
        end
        Core[Core Network]
        Transport[Transport Network]
        Slices[Network Slices]
    end

    %% Automated Verification
    Test[Automated Verification]

    %% Flows
    UI -->|Select Use Case| Controller
    UC1 --> Controller
    UC2 --> Controller
    UC3 --> Controller

    Config -->|Load Profiles & Slices| Controller
    Controller -->|Apply Config| gNB
    Controller -->|Apply Config| Core
    Controller -->|Apply Config| Transport
    Controller -->|Activate Slices| Slices
    Controller -->|Run Tests| Test
    Test -->|Results| UI

    %% Styling
    classDef network fill:#e0f7fa stroke:#00796b stroke-width:2px
    class Network,RAN_Sub,Slices network

    classDef ui fill:#fff9c4 stroke:#fbc02d stroke-width:2px
    class UI,UseCases ui

    classDef controller fill:#c5cae9 stroke:#303f9f stroke-width:2px
    class Controller controller

    classDef test fill:#ffccbc stroke:#bf360c stroke-width:2px
    class Test test
