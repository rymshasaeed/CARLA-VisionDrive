# CARLA Live VisionDrive
A Python-based autonomous driving simulation that integrates **CARLA** with **YOLOv7** for real-time object detection. The system captures camera frames from an ego vehicle, performs live object detection, and displays the annotated output inside a PyGame window while driving through the simulated environment.

The project can also be synchronized with **SUMO (Simulation of Urban MObility)** to create realistic traffic scenarios for autonomous driving research and testing.

### Features
- Real-time object detection using YOLOv7
- Live camera stream from the CARLA ego vehicle
- PyGame visualization window
- Multiple pre-trained YOLOv7 ONNX models included
- CARLA–SUMO synchronization support
- Traffic simulation with configurable NPC vehicles
- Modular project structure for extending sensors and perception

### Project Structure
```
CARLA/
    obj-det.py
    weights/
    yolo/

Sumo/
    run_synchronization.py
    spawn_npc_sumo.py
    examples/
    sumo_integration/

utils/
    sensors.py
    spawnSensors.py
    spawnClosestTo.py
    weatherList.py

main.py
```

### Requirements
- Windows OS
- Python 3.7
- CARLA 0.9.8
- SUMO 1.22.0 (optional, for traffic synchronization)


## Running Object Detection
Launch the CARLA simulator first, then execute:
```bash
python main.py
```
A PyGame window will open showing the live camera stream from the ego vehicle with real-time object detection overlays.

User can also select which YOLOv7 model to use by updating the model path in `main.py`. The repository includes multiple ONNX versions of YOLOv7 and YOLOv7-Tiny for different input resolutions:

- yolov7-tiny_256×320
- yolov7-tiny_384×640
- yolov7-tiny_480×640
- yolov7-tiny_736×1280
- yolov7_256x480
- yolov7_256x640
- yolov7_384x640
- yolov7_640x640
- yolov7_736x1280

Choose the model depending on the required balance between detection precision and inference speed.

## Running CARLA + SUMO Co-Simulation
1. Start the CARLA client first.
2. To synchronize SUMO with CARLA:
```bash
python SUMO/run_synchronization.py examples/Town01.sumocfg --sumo-gui
```
3. To spawn traffic:
```bash
python SUMO/spawn_npc_sumo.py -n 10 --tls-manager carla --sumo-gui
```
This creates synchronized traffic between CARLA and SUMO, allowing the ego vehicle to interact with realistic traffic while object detection continues in real time.

### Workflow
1. Launch CARLA.
2. Spawn the ego vehicle.
3. Manually drive the ego vehicle, or toggle automatic driving.
4. Capture frames in real time.
5. Perform YOLOv7 inference.
6. Draw bounding boxes and class labels.
7. Display the annotated output in the PyGame window.
8. (Optional) Synchronize with SUMO to simulate realistic traffic.

### Notes
- Designed for CARLA 0.9.8.
- Python 3.7 is recommended.
- Ensure the CARLA server is running before starting the object detection client.
- SUMO integration is optional but recommended for realistic traffic scenarios.
