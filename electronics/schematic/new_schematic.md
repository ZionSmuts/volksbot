# New Electronics Schematic

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

```

# New Volksbot Schematic – Description  

The updated schematic replaces the old pair of lead-acid batteries with a **Booant 24 V / 30 Ah LiFePO₄ battery pack**. This upgrade reduces weight, increases runtime, and simplifies the power system to a single 24 V source. A **50 A DC fuse** is installed close to the battery on the positive line to provide main protection against short circuits. From there, power is routed into the **front distribution panel** through a **Phoenix Contact PC 4/2-STF-7.62 connector**, while the negative lead runs directly to the ground bus.  

<p float="center">
  <img src="/images/PC4-2-STF-7,62-pcb-connector.jpg" width="250"/>
  <img src="/images/CAN-wire-j8-to-j8.jpg" width="250"/>
  <img src="/images/connection-with-female-plug-PC5-2-GF-7,62.jpg" width="250"/>
</p>


Inside the distribution panel, power is split into separate fused outputs:  

- **Out 1 (24 V):** Feeds EPOS2 motor controller #1, protected with a 15 A fuse (can be raised to 20 A if nuisance trips occur).  
- **Out 2 (24 V):** Feeds EPOS2 motor controller #2, also protected with its own 15 A fuse.  
- **Out 3 (24 V):** Reserved for future peripherals, to be fused when needed.  
- **Out 4 (12 V, 5 A):** Supplies the NVIDIA Jetson AGX Xavier (Auvidea X221 carrier board).  
- **Out 5 (5 V, 5 A):** Reserved for future low-voltage peripherals.  

The **emergency stop (E-stop)** line controls the main relay. When pressed, it disconnects the battery from the distribution panel, cutting off all outputs at once — including the Jetson and both motor controllers. This ensures a safe and immediate shutdown.  

On the control side, the **Jetson AGX Xavier** acts as the “brain” of the system. It connects to the two EPOS2 controllers over **CAN bus** using a USB-to-CAN adapter. The adapter connects first to EPOS2 #1 (port J7), which is daisy-chained to EPOS2 #2 (port J8). CAN termination is applied properly: disabled on EPOS2 #1, enabled on EPOS2 #2, and provided on the adapter side. The CAN ground is tied into the system ground at the panel, keeping the communication stable.  

The **motors are unfused** in this design, since each EPOS2 motor controller already provides current and fault protection for its motor output.

<p align="center">
  <img src="/images/NVIDIA-Jetson-Xavier-AGX-X221.jpg" alt="Old Wiring Setup" width="350"/>
</p>

