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

---

## Wiring inside the Volksbot

Here below is what I saw for the first time when opening up the Volksbot. It was quite messy, but I managed to take out every component and see where each connection was made.

<p align="center">
  <img src="images/old-wiring-setup.jpg" alt="Old Wiring Setup" width="450"/>
</p>

From this, I managed to make a schematic diagram and could only assume that a laptop was used as the "brain" of the whole system.

Other things that I found were that the lead-acid batteries were completely dead. Hence, that was the reason why I decided to go for an upgrade to a 24V LiPo battery instead of two 12V batteries connected in series.

Fortunately, the good things that I got from the old design were the chassis, motors, and motor controllers, which I had tested — and to my surprise, they were still working. So it was up to me to find a replacement for the "brain" of the whole system.

To my luck, the company gave me the NVIDIA Jetson AGX Xavier to use on the Volksbot, and I’m quite excited to start using it!

**NOTE:** I will make sure to also add a step-by-step breakdown in the future on how I use the Jetson, but also my approach to simulating the Volksbot in Gazebo :)
