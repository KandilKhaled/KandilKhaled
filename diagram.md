flowchart TD
    %% User Interface
    UI[User Interface<br/>(Web/GUI Dashboard)<br/>Issue 2.4]
    
    %% Controller / Backend
    Controller[Controller / Backend<br/>Handles use case selection, config, actions<br/>Issues 2.3, 2.4]

    %% Configuration Module
    Config[Configuration Module<br/>(Use Cases, Profiles, Slices)<br/>Issue 2.4]

    %% Network Components
    subgraph Network["5G Network Components"]
        subgraph RAN_Sub["RAN"]
            gNB[gNodeB (gNB)<br/>Issue 4.3]
            UE[UE Simulator (optional)]
        end
        Core[Core Network<br/>Issue 4.3]
        Transport[Transport Network<br/>Issue 5.3]
        Slices[Network Slices<br/>(Slice Name, Priority, Bandwidth)<br/>Issue 5.2]
    end

    %% Automated Verification
    Test[Automated Verification Module<br/>(Run test scripts, return results)<br/>Issue 5.4]

    %% Use Cases
    subgraph UseCases["Use Case Selection<br/>Issue 2.3"]
        UC1[Industrial IoT]
        UC2[Connected Cars]
        UC3[Smart City]
    end

    %% Flows
    UI -->|Select Use Case| Controller
    UC1 --> Controller
    UC2 --> Controller
    UC3 --> Controller

    Config -->|Load Configs & Slices| Controller
    Controller -->|Apply Config| gNB
    Controller -->|Apply Config| Core
    Controller -->|Apply Config| Transport
    Controller -->|Activate Slices| Slices
    Controller -->|Trigger Tests| Test
    Test -->|Results| UI

    %% Styling
    classDef network fill:#e0f7fa,stroke:#00796b,stroke-width:2px
    class Network,RAN_Sub,Slices network

    classDef ui fill:#fff9c4,stroke:#fbc02d,stroke-width:2px
    class UI,UseCases ui

    classDef controller fill:#c5cae9,stroke:#303f9f,stroke-width:2px
    class Controller controller

    classDef test fill:#ffccbc,stroke:#bf360c,stroke-width:2px
    class Test test
