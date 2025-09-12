# Electronics Schematic

```mermaid
flowchart TD

%% ===================
%% BATTERY + PROTECTION
%% ===================
subgraph Power["Power Source & Protection"]
    Battery["24V 30Ah Battery"]
    FuseMain["6 mm² KFZ Fuse"]
    FrontPanel["Front Panel"]
    Battery -->|6 mm²| FuseMain --> FrontPanel
end

%% ===================
%% DISTRIBUTION
%% ===================
subgraph Distribution["Power Distribution"]
    Out1["Out 1: Ext Power 24V / 20A"]
    Out2["Out 2: 24V / 20A"]
    Out3["Out 3: 12V / 5A"]
    Out4["Out 4: 5V / 5A"]
    EStopConn["Emergency Stop Line"]

    FrontPanel --> Out1
    FrontPanel --> Out2
    FrontPanel --> Out3
    FrontPanel --> Out4
    FrontPanel --> EStopConn
end

%% ===================
%% DRIVE TRAIN
%% ===================
subgraph Drive["Motor Drive Train"]
    EPOS1["EPOS2 Controller #1"]
    EPOS2["EPOS2 Controller #2"]
    Motor1["Maxon Motor #1"]
    Motor2["Maxon Motor #2"]
    Encoder1["Encoder #1"]
    Encoder2["Encoder #2"]

    Out1 -->|2.5 mm² Fuse| EPOS1
    Out2 -->|2.5 mm² Fuse| EPOS2

    EPOS1 -->|Motor Cable #1| Motor1
    EPOS2 -->|Motor Cable #2| Motor2

    Motor1 --> Encoder1 --> EPOS1
    Motor2 --> Encoder2 --> EPOS2
end

%% ===================
%% CONTROL
%% ===================
subgraph Control["Control System"]
    Jetson["NVIDIA Jetson Xavier AGX"]
    CAN["USB–CAN Adapter"]
    TermLoop["Termination Loop"]

    Out3 -->|2 mm² Fuse| Jetson
    Jetson --> CAN --> EPOS1 --> EPOS2 --> TermLoop
end

%% ===================
%% SAFETY
%% ===================
subgraph Safety["Safety"]
    EStop["Emergency Stop"]
    EStopConn -->|4 mm²| EStop
end

%% ===================
%% COLORS
%% ===================
style Power fill:#fff3b0,stroke:#333,stroke-width:2px
style Distribution fill:#b0e57c,stroke:#333,stroke-width:2px
style Drive fill:#add8e6,stroke:#333,stroke-width:2px
style Control fill:#dcb0f2,stroke:#333,stroke-width:2px
style Safety fill:#f2b0b0,stroke:#333,stroke-width:2px
