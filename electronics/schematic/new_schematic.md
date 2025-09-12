# New Power Electronics Schematic

```mermaid
flowchart TB
  %% Styles
  classDef fuse fill:#ffe0e0,stroke:#b00;
  classDef panel fill:#e0ffe0,stroke:#0b0;
  classDef comp fill:#e0f0ff,stroke:#00b;
  classDef motor fill:#fef7d1,stroke:#aa0;
  classDef io fill:#f6f6d5,stroke:#999;

  %% Battery and main fuse
  BAT[24V 30Ah Battery]:::comp
  FUSE_MAIN[50A Fuse (6 mm²)]:::fuse
  BAT --> FUSE_MAIN

  %% Front Panel
  FUSE_MAIN --> PANEL[Front Panel]:::panel

  %% Panel outputs
  PANEL -->|Out 1: 24V/20A| FUSE1[2.5 mm² KFZ Fuse]:::fuse --> EPOS1[EPOS2 70/10 #1]:::comp
  PANEL -->|Out 2: 24V/20A| FUSE2[2.5 mm² KFZ Fuse]:::fuse --> EPOS2[EPOS2 70/10 #2]:::comp
  PANEL -->|Out 3: 12V/5A| FUSE3[2 mm² Fuse]:::fuse --> JET[Jetson AGX Xavier]:::comp
  PANEL -->|Out 4: 5V/5A| OUT4[(Reserved)]:::comp
  PANEL -->|Emergency Stop| ESTOP[E-Stop Relay]:::comp

  %% Motors
  EPOS1 --> M1[Maxon Motor 241144 #1]:::motor
  EPOS2 --> M2[Maxon Motor 241144 #2]:::motor

  %% CAN Bus
  JET -. USB-to-CAN .-> USB[USB–CAN Adapter]:::io
  USB --- EPOS1
  EPOS1 --- EPOS2
  EPOS2 -. Termination .- EPOS2

  %% Encoders (optional representation)
  M1 -. Encoder #1 .-> EPOS1
  M2 -. Encoder #2 .-> EPOS2
