# System Architecture Diagram

```mermaid
flowchart TB
    %% User Interface
    UI[UI - Web GUI]

    %% Use Cases
    subgraph UseCases["Use Case Selection"]
        UC1[Industrial_IoT]
        UC2[Connected_Cars]
        UC3[Smart_City]
    end

    %% Controller / Backend
    Controller[Controller_Backend]

    %% Configuration Module
    Config[Configuration_Module]

    %% Network Components
    subgraph Network["5G Network Components"]
        subgraph RAN_Sub["RAN"]
            gNB[gNodeB]
            CU[Central_Unit_CU]
            DU[Distributed_Unit_DU]
            gNB --> CU
            CU --> DU
        end
        Core[Core_Network]
        Transport[Transport_Network]
        Slices[Network_Slices_QoS]
    end

    %% Automated Verification
    Test[Automated_Verification]

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
