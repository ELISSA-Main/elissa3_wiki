# Optitrack

The Optitrack system captures the position of the freeflyers.

---

Table of Content:
- [Optitrack](#optitrack)
  - [Recalibrating Optitrack](#recalibrating-optitrack)

---
## Recalibrating Optritrack

This guide provides a step by step description of the process required to recalibrate the Optritrack system.<br>
See https://v20.wiki.optitrack.com/index.php?title=Calibration as a reference.

1. Remove all objects with reflectors from the table and make sure none are visible from the control center.
2. Reset the application settings (Edit > Reset Application Settings). <img src="wiki/graphics/reset calibration.png" alt="Reset Calibration" width="400">
3. Then go to "Application Settings" pane and set the "Continuous Calibration" setting as "Continuous". <img src="wiki/graphics/application settings.png" alt="Application Settings" width="300"> <img src="wiki/graphics/continuous calibration.png" alt="Continuous Calibration" width="600">
4. Set a small FPS for calibration, EXP 250, THR 200, LED 15. <br> <img src="wiki/graphics/calibration camera parameters.png" alt="Camera Parameters" width="400">
5. In the Camera Calibration Pane, set the OptiWand in the Calibration Options as Micron Series, and the Wand Length(mm) is set as 249.864 for our calibration device. <br> <img src="wiki/graphics/camera calibration pane.png" alt="Camera Calibration Pane" width="300"> <img src="wiki/graphics/OptiWand.png" alt="Optiwand" width="600">
6. Click the button "Clear Mask", then click the button "Mask Visible".<img src="wiki/graphics/Clear Mask Mask Visible.png" alt="Mask Options" width="700">
7. Click the button "Start Wanding" and start wanding until all cameras show a green calibration status on their rim using the OptiWand.
8. Calculate the calibration quality when sufficient data is obtained.
9. Set the vertical offset of the calibration square (CS-200) for our motion capture system to 19 mm. Press the button "Set Ground Pane". <br> <img src="wiki/graphics/CS-200.png" alt="CS-200" width="600"> <br> Visit https://v20.wiki.optitrack.com/index.php?title=Calibration_Squares for further information on calibration squares.<br>
10. In new calibration: View – Data Streaming Pane
      - Activate “Broadcast Frame Data”,
      - Activate “Broadcast VRPN Data”
      - Set the Up axis to “Z up” 
11. Redefine rigid bodies:
      - mark the reflectors at the upper 4 corners of an object 
      - select: right click - rigid body - create from selected markers
      - rename the object: bsp.: vrpn/hannibal
      - add all remaining reflectors of the object to the rigid body by marking them together with the already defined ones


---
 
