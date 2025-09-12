# Old Power Electronics Schematic

```mermaid
flowchart TB
  %% Styles
  classDef fuse fill:#ffe0e0,stroke:#b00;
  classDef panel fill:#e0ffe0,stroke:#0b0;
  classDef comp fill:#e0f0ff,stroke:#00b;
  classDef motor fill:#fef7d1,stroke:#aa0;
  classDef io fill:#f6f6d5,stroke:#999;

  %% Battery pack (lead acid)
  B1[12V Panasonic SLA #1]:::comp
  B2[12V Panasonic SLA #2]:::comp
  B1 --- B2
  BATT24[(~24V from 2×12V SLA)]:::comp
  B2 --> BATT24

  %% Main fuse
  FUSE_MAIN[Main Fuse (?A)]:::fuse
  BATT24 --> FUSE_MAIN

  %% Front panel
  FUSE_MAIN --> PANEL[Front Panel]:::panel

  %% Outputs
  PANEL -->|Out 1: 24V| EPOS1[EPOS2 70/10 #1]:::comp
  PANEL -->|Out 2: 24V| EPOS2[EPOS2 70/10 #2]:::comp
  PANEL -->|Out 3: ?V| LAPTOP[Laptop (assumed)]:::comp
  PANEL -->|Out 4: ?V| LIDAR[Lidar Camera (removed later)]:::comp
  PANEL -->|Emergency Stop| ESTOP[E-Stop Relay]:::comp

  %% Motors
  EPOS1 --> M1[Maxon Motor 241144 #1]:::motor
  EPOS2 --> M2[Maxon Motor 241144 #2]:::motor

  %% CAN bus (no adapter)
  EPOS1 --- EPOS2
  EPOS1 -. Termination .- EPOS1
  EPOS2 -. Termination .- EPOS2

  %% Encoders
  M1 -. Encoder #1 .-> EPOS1
  M2 -. Encoder #2 .-> EPOS2
