# Collaborative Agricultural Monitoring and Spraying Drones

This project features a two-drone autonomous swarm designed for precision agriculture. The system uses a **Scanner Drone** to find crop issues and a **Sprayer Drone** to treat them with centimeter-level accuracy.

---



##  Drone 1: The Scanner
A custom 3D-printed quadcopter that acts as the "eyes" of the operation.

* **Compute:** NVIDIA Jetson Orin for onboard edge processing.
* **Navigation:** Cube Orange+ with Here 4 GPS and RTK for high-precision geotagging.
* **Vision:** Siyi A8 mini camera on a 3-axis gimbal.
* **Logic:** Uses HSV filtering to find yellow leaves. It converts image pixels into GPS coordinates by calculating the drone's altitude and attitude (tilt).

---

##  Drone 2: The Sprayer
A heavy-lift quadcopter with a 10L capacity and dual nozzle system for spraying.

* **Compute:** Raspberry-Pi 5 handling coordination and nozzle logic.
* **System:** 110 PSI high-pressure pump with custom 3D-printed dual nozzles (Wide/Precise).
* **Hardware:** Custom-made PCB to trigger the spray based on script commands.
* **Precision:** Once at the GPS location, it uses a **Visual Centering Script**. It calculates the error between the yellow spot and the center of the frame to position itself perfectly before spraying.
* **Wind Resistance:** The precise nozzle is positioned in a way that 10L tank blocks the propeller downwash, ensuring the spray hits the target accurately.

---

##  System Workflow:
1.  **Search:** The Scanner flies over the field and "pins" every yellow leaf it sees with a GPS tag.
2.  **Plan:** The coordinates are clustered to decide which nozzle the Sprayer should use.
3.  **Action:** The Sprayer flies to the pins, centers itself using its own camera, and activates the high-pressure pump.

---

##  Repository Contents
* : Python code for Jetson Orin (HSV filtering & GPS conversion).
* : Python code for Raspberry Pi (Centeri & PCB control).
* : 3D STL files for the chassis and nozzles, plus PCB schematics.
