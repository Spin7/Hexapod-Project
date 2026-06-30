# Hexapod Project — ROS2 Package
<p align="center">
  <img src="Hexapod.jpg" alt="The hexapod robot" width="700">
</p>

> **Part of the [Hexapod Project](https://github.com/Spin7/Hexapod-Project)**  
> This folder contains the full ROS2 package (`hexapod_pkg`) for both **Gazebo simulation** and **real robot** operation.

---

## Reference Setup

| Component | Hardware | OS |
|---|---|---|
| 🖥️ **PC** | ASUS TUF Gaming F15 (NVIDIA RTX 3060) | Ubuntu 24.04 LTS |
| 🍓 **Raspberry Pi** | Raspberry Pi 4 — 4 GB RAM | Ubuntu 24.04 LTS |
| 📱 **Smartphone** | Google Pixel 7 | Android (sensors + camera) |
| 🔌 **Microcontroller** | Arduino Mega | — |

> **Note (YOLO & GPU):** A dedicated GPU is **strongly recommended** for real-time YOLO-based vision. Without one, detection will still work but with limited performance.

---

## 1. PC Installation

### 1.1. Install ROS2

Choose the version that matches your Ubuntu distribution:

| Ubuntu | ROS2 Distribution |
|---|---|
| 22.04 | [ROS2 Humble](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html) |
| 24.04 | [ROS2 Jazzy](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debians.html) *(Recommended)* |
| 24.04 | [ROS2 Rolling](https://docs.ros.org/en/rolling/Installation/Ubuntu-Install-Debians.html) |

---

### 1.2. Install build tools

```bash
sudo apt update
sudo apt install python3-colcon-common-extensions
```

---

### 1.3. Source ROS2 and colcon permanently

```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
source ~/.bashrc
```

> **OBS:** Replace `jazzy` with your distribution (`humble`, `rolling`, etc.)

---

### 1.4. Install Gazebo (Harmonic) and the ROS2–Gazebo bridge

```bash
sudo apt install ros-jazzy-ros-gz
```

> **OBS:** Replace `jazzy` with your ROS2 distribution. This installs `ros_gz_sim`, `ros_gz_bridge`, and all related packages needed for simulation.

---

### 1.5. Install IriunWebCam (phone camera support)

```bash
wget https://iriun.gitlab.io/iriunwebcam-2.9.deb
sudo apt install ./iriunwebcam-2.9.deb
sudo apt --fix-broken install
```

---

### 1.6. Check GPU / CUDA support *(skip if no GPU)*

```bash
nvidia-smi
```

Expected output when GPU is ready:

```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 510.79.02    Driver Version: 510.79.02    CUDA Version: 11.6     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
...
+-----------------------------------------------------------------------------+
```

If the command fails, install NVIDIA drivers via Ubuntu autodetect:

```bash
sudo apt update
sudo apt install ubuntu-drivers-common
sudo ubuntu-drivers autoinstall
sudo reboot
```

---

### 1.7. Create a Python virtual environment for YOLO

```bash
python3 -m venv ~/.venvs/yolo
source ~/.venvs/yolo/bin/activate
```

> **OBS:** Always activate this environment in a **separate terminal** from the one running the ROS2 nodes.

---

### 1.8. Install YOLO dependencies inside the virtual environment

```bash
pip install torch torchvision torchaudio
pip install ultralytics
pip install opencv-python
```

---

### 1.9. Install OpenCV system-wide (for ROS2 nodes)

```bash
sudo apt install python3-opencv
```

---

### 1.10. Create the ROS2 workspace

```bash
mkdir -p ~/ros2_hexapod_ws/src
cd ~/ros2_hexapod_ws/src
```

---

### 1.11. Clone the repository

```bash
git clone https://github.com/Spin7/Hexapod-Project.git
```

The ROS2 package lives inside the cloned repo at:

```
Hexapod-Project/
└── 1_ROS2_Gazebo_Project/
    └── hexapod_pkg/      ← the colcon package
```

Copy only the package into the workspace `src/` so colcon can find it:

```bash
cp -r ~/ros2_hexapod_ws/src/Hexapod-Project/1_ROS2_Gazebo_Project/hexapod_pkg \
      ~/ros2_hexapod_ws/src/
```

---

### 1.12. Build the workspace

```bash
cd ~/ros2_hexapod_ws
colcon build --symlink-install
```

---

### 1.13. Source the workspace permanently

```bash
echo "source ~/ros2_hexapod_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 2. Raspberry Pi Installation

### 2.1. Install ROS2

Same as PC — choose based on your Ubuntu version (see [step 1.1](#11-install-ros2)).

---

### 2.2. Install build tools

```bash
sudo apt update
sudo apt install python3-colcon-common-extensions
```

---

### 2.3. Source ROS2 and colcon permanently

```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
source ~/.bashrc
```

> **OBS:** Replace `jazzy` with your ROS2 distribution.

---

### 2.4. Install hardware interface dependencies

```bash
sudo apt update
sudo apt install python3-smbus
sudo apt install python3-smbus2
sudo apt install python3-rpi.gpio
sudo apt install python3-serial
sudo apt install python3-opencv
```

---

### 2.5. Create the ROS2 workspace

```bash
mkdir -p ~/ros2_hexapod_ws/src
cd ~/ros2_hexapod_ws/src
```

---

### 2.6. Clone the repository

```bash
git clone https://github.com/Spin7/Hexapod-Project.git
```

Copy the package into the workspace `src/`:

```bash
cp -r ~/ros2_hexapod_ws/src/Hexapod-Project/1_ROS2_Gazebo_Project/hexapod_pkg \
      ~/ros2_hexapod_ws/src/
```

---

### 2.7. Build the workspace

```bash
cd ~/ros2_hexapod_ws
colcon build --symlink-install
```

---

### 2.8. Source the workspace permanently

```bash
echo "source ~/ros2_hexapod_ws/install/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 3. Running the Package

The system is launched in layers. Each mode requires specific launches to be started **in order**.

### 3.1. Simulation (PC only)

```bash
# Terminal 1 — MANDATORY: start Gazebo + spawn robot
ros2 launch hexapod_pkg gazebo_hexapod_sim.launch.py

# Terminal 2 — optional (required for navigation modes)
ros2 launch hexapod_pkg sensors_compute_sim.launch.py

# Terminal 3 — pick ONE operation mode:
ros2 launch hexapod_pkg navigation_to_target_sim.launch.py  # Autonomous navigation
ros2 launch hexapod_pkg follower_sim.launch.py              # Vision-based follower
ros2 launch hexapod_pkg swarm_follower_sim.launch.py        # Swarm follower
ros2 launch hexapod_pkg social_robot_sim.launch.py          # Hand gesture control
```

### 3.2. Real Robot (PC + Raspberry Pi)

**On the Raspberry Pi:**
```bash
# Terminal 1 — MANDATORY: read hardware sensors
ros2 launch hexapod_pkg read_sensors_rasberrypi.launch.py
```

**On the PC:**
```bash
# Terminal 1 — MANDATORY: DDS bridge to Arduino
ros2 launch hexapod_pkg dds_comunication.launch.py

# Terminal 2 — optional (required for navigation modes)
ros2 launch hexapod_pkg sensors_compute_real.launch.py

# Terminal 3 — pick ONE operation mode:
ros2 launch hexapod_pkg navigation_to_target_real.launch.py # Autonomous navigation
ros2 launch hexapod_pkg follower_real.launch.py             # Vision-based follower
ros2 launch hexapod_pkg swarm_follower_real.launch.py       # Swarm follower
ros2 launch hexapod_pkg social_robot_real.launch.py         # Hand gesture control
```

---

## 4. Package Structure

```
hexapod_pkg/
├── config/                         # ROS2 parameters and bridge config (gz_bridge.yaml)
├── description_hexapod/            # URDF/XACRO robot model
├── hexapod_pkg/                    # Python source nodes
│   ├── dds_nodes/                  # DDS communication (PC ↔ Arduino)
│   ├── gazebo_nodes/               # Gazebo-specific control and IR emulation
│   ├── localization_and_orientation_nodes/  # GPS, heading, dead-reckoning
│   ├── sensors_interfaces_nodes/   # Ultrasonic sensor processing
│   ├── master_nodes/               # System health monitor
│   ├── camera_nodes/               # WebCam node
│   ├── image_recognition_nodes/    # YOLO and classic vision detectors
│   ├── teleop_nodes/               # Keyboard / manual control
│   ├── navigation_nodes/           # Autonomous navigation planners
│   ├── social_robot_nodes/         # Gesture-based HRI
│   ├── read_sensors_nodes/         # Hardware sensor readers (Raspberry Pi)
│   └── auto_balance_nodes/         # Balance controller
├── launch/                         # Real robot launches (PC side)
├── launch_pi/                      # Real robot launches (Raspberry Pi side)
├── launch_sim/                     # Simulation launches
├── meshes/                         # 3D mesh files
├── models/                         # Gazebo model definitions
├── worlds/                         # Gazebo world files
├── CMakeLists.txt
└── package.xml
```






