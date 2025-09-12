# New Electronics Schematic

```mermaid
flowchart TB

  %% Nodes
  BAT[24V 30Ah Battery]
  FUSE_MAIN[50A Fuse (6 mm2)]
  PANEL[Front Panel]

  %% Battery -> Panel
  BAT --> FUSE_MAIN
  FUSE_MAIN --> PANEL

  %% Panel outputs
  PANEL -->|Out 1: 24V / 20A| EPOS1[EPOS2 70/10 #1]
  PANEL -->|Out 2: 24V / 20A| EPOS2[EPOS2 70/10 #2]
  PANEL -->|Out 3: 12V / 5A| JET[Jetson AGX Xavier]
  PANEL -->|Out 4: 5V / 5A| OUT4[Reserved]
  PANEL -->|Emergency Stop| ESTOP[E-Stop Relay]

  %% Motors
  EPOS1 --> M1[Maxon Motor 241144 #1]
  EPOS2 --> M2[Maxon Motor 241144 #2]

  %% CAN / control
  JET -. USB to CAN .-> USB[USB to CAN Adapter]
  USB --- EPOS1
  EPOS1 --- EPOS2

  %% Encoders
  M1 -. Encoder #1 .-> EPOS1
  M2 -. Encoder #2 .-> EPOS2
