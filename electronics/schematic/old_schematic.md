# Old Electronics Schematic

```mermaid
flowchart TD

%% ===================
%% BATTERY + PROTECTION
%% ===================
subgraph Power["Power Source & Protection"]
    Batt1["Panasonic SLA 12V"]
    Batt2["Panasonic SLA 12V"]
    FuseMain["Main Fuse"]
    FrontPanel["Front Distribution Panel"]

    Batt1 -->|12V| Batt2
    Batt2 -->|=24V| FuseMain --> FrontPanel
end

%% ===================
%% DISTRIBUTION (same as new schematic)
%% ===================
subgraph Distribution["Power Distribution"]
    Out1["Out 1: EPOS2 Controller #1"]
    Out2["Out 2: EPOS2 Controller #2"]
    Out3["Out 3: Peripherals"]
    Out4["Out 4: 12V / 5A"]
    Out5["Out 5: 5V / 5A"]
    EStopConn["Emergency Stop Line"]

    FrontPanel --> Out1
    FrontPanel --> Out2
    FrontPanel --> Out3
    FrontPanel --> Out4
    FrontPanel --> Out5
    FrontPanel --> EStopConn
end

%% ===================
%% CONTROL (centered)
%% ===================
subgraph Control["Control System"]
    direction TB
    Laptop["Laptop Controller"]
    Lidar["Lidar Sensor"]

    Laptop -->|USB| EPOS1
    Laptop -->|USB| Lidar
    Out5 --> Lidar
end

%% ===================
%% DRIVE TRAIN
%% ===================
subgraph Drive["Motor Drive Train"]
    direction LR
    EPOS1["EPOS2 Controller #1"]
    EPOS2["EPOS2 Controller #2"]
    Motor1["Maxon Motor #1"]
    Motor2["Maxon Motor #2"]
    Encoder1["Encoder #1"]
    Encoder2["Encoder #2"]

    Out1 --> EPOS1 --> Motor1 --> Encoder1 --> EPOS1
    Out2 --> EPOS2 --> Motor2 --> Encoder2 --> EPOS2

    EPOS1 <--> EPOS2
    EPOS1 -. Daisy-chain CAN .- EPOS2
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