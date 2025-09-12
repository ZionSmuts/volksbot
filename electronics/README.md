## Welcome to the Electronics folder!

Here in this folder, I will share with you the schematic diagrams of both the old and new electronics layouts. Please find them in the `/schematic` section of this folder.

There you can see all the connections between components and how the power electronics “talk” to each other as well.

---

## What is the main difference between the old and new schematic diagrams?

Even though you may see similarities in some components and connections, I did make changes where upgrades were necessary. Those changes include:

- **Battery upgrade:** Swapping out the Panasonic lead-acid batteries (12V) connected in parallel to create 24V for much more energy-efficient 24V LiFePO₄ batteries from BOOANT. This decreases the weight of the Volksbot by around 2.0 kg, which helps with carrying more load in the future, while also offering better battery memory (longer usable life and cycles).
- **Jetson integration:** Adding the NVIDIA Jetson AGX Xavier — an incredibly powerful module used widely in robotics where high processing power is needed. I believe this replaced a laptop that used to sit on top of the Volksbot, but since there was no documentation and it was already removed when I first saw the Volksbot, this is only an assumption.
- **CAN communication:** Adding a PCAN-USB adapter to connect the Jetson to the EPOS motor controllers. Previously, there was already CAN bus communication between the controllers, but I was unsure how they managed it. The controllers were directly daisy-chained with termination loops on both CAN ports, leaving no port free for a computer to connect. Perhaps the laptop was connected to the controllers via USB, but that’s only an assumption. I added this adapter to make sure the setup makes sense and all pieces are connected properly.
- **Removed lidar camera:** One thing I removed in the new design was the lidar camera on top of the Volksbot. Since I’ll be controlling the rover with a joystick, I don’t necessarily need lidar right now. Of course, this will change if I want to make the Volksbot autonomous in the future, but that’s a challenge for another time.

Other than these, the connections remain very similar — especially with the Power Distribution Unit (PDU) in the front. I’m very fortunate that it still works, because the company Fraunhofer no longer makes them. So for anyone looking to create a similar PDU, it’s best to check tutorials on YouTube to see how to build one yourself.

---

## Wiring and Images

In this section, I will include photos showing how the wiring looked originally and provide a better description of how I chose the fuse ratings and wire thickness for each part of the schematic.  
**TBC**
