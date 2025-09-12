# New Electronics Schematic

<pre> ```

flowchart TD
  Battery["24V 30Ah Battery"] -->|6 mm²| FrontPanel["Front Panel"]
  
  FrontPanel -->|2.5 mm² Fuse| EPOS1["EPOS2 Motor Controller 70/10\n#1 (37571111)"]
  FrontPanel -->|2.5 mm² Fuse| EPOS2["EPOS2 Motor Controller 70/10\n#2 (37571111)"]
  FrontPanel -->|2 mm² Fuse| Jetson["NVIDIA Jetson Xavier AGX"]
  FrontPanel -->|4 mm²| EStop["Emergency Stop"]

  EPOS1 -->|Motor Cable #1| Motor1["Maxon Motor 241414\n#1"]
  EPOS2 -->|Motor Cable #2| Motor2["Maxon Motor 241414\n#2"]

  Motor1 -->|Encoder #1| EPOS1
  Motor2 -->|Encoder #2| EPOS2

  Jetson --> USB_CAN["USB–CAN Adapter"]
  USB_CAN -->|CAN Cable| EPOS1
  EPOS1 -->|CAN Cable| EPOS2

  EPOS2 --> TermLoop["Termination Loop"]


```</pre>
