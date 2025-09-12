# Old Electronics Schematic

```mermaid
flowchart TB
  %% Styles
  classDef fuse fill:#ffe0e0,stroke:#b00;
  classDef panel fill:#e0ffe0,stroke:#0b0;
  classDef comp fill:#e0f0ff,stroke:#00b;
  classDef motor fill:#fef7d1,stroke:#aa0;

  %% Battery pack (lead acid)
  B1[12V Panasonic SLA #1]:::comp
  B2[12V Panasonic SLA #2]:::comp
  B1 --- B2
  BATT24[~24V (2x 12V SLA in series)]:::comp

  %% Main fuse + panel
  FUSE_MAIN[Main Fuse (?A)]:::fuse
  B2 --> BATT24 --> FUSE_MAIN --> PANEL[Front Panel]:::panel

  %% Outputs (assumed)
  PANEL -->|Out 1: 24V| EPOS1[EPOS2 70/10 #1]:::comp
  PANEL -->|Out 2: 24V| EPOS2[EPOS2 70/10 #2]:::comp
  PANEL -->|Out 3: 12V|  LAPTOP[Laptop (assumed)]:::comp
  PANEL -->|Out 4: 5V|  LIDAR[Lidar Camera]:::comp
  PANEL -->|Emergency Stop| ESTOP[E-Stop Relay]:::comp

  %% Motors
  EPOS1 --> M1[Maxon Motor 241144 #1]:::motor
  EPOS2 --> M2[Maxon Motor 241144 #2]:::motor

  %% CAN bus (no external adapter; both ends terminated)
  EPOS1 -. Termination ON .- EPOS1
  EPOS1 --- EPOS2
  EPOS2 -. Termination ON .- EPOS2
