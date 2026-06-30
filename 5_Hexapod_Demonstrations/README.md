# 🎬 Hexapod Demonstrations

<p align="center">
  <img src="Hexapod_real_and_sim.png" alt="Hexapod — Real robot and Gazebo simulation" width="860">
</p>

<p align="center">
  <em>Left: Physical robot in the real world · Right: Gazebo simulation counterpart</em>
</p>

> **Part of the [Hexapod Project](https://github.com/Spin7/Hexapod-Project)**  
> This folder contains all video demonstrations of the hexapod robot operating in both **Gazebo simulation** and on the **real hardware** (Raspberry Pi + Arduino Mega).

---

## 📂 Structure

```
5_Hexapod_Demonstrations/
├── Simulation Robot Demonstrations/    # 7 Gazebo / ROS2 videos
├── Real Robot Demonstrations/          # 9 physical robot videos
└── Hexapod_real_and_sim.png            # Hero comparison image
```

---

## 🎮 Simulation Demonstrations — 7 Videos

> 📁 [`Simulation Robot Demonstrations/`](Simulation%20Robot%20Demonstrations/README.md)  
> 🎬 YouTube Playlist: **Hexapod Project — Simulation (Gazebo + ROS2)**

All behaviors run inside **Gazebo Harmonic** with **ROS2 Jazzy**. No hardware required — perfect for understanding the software architecture before deploying to real hardware.

| # | Video File | Mode | YouTube |
|---|---|---|---|
| 1 | `1_Hexapod_gazebo_launch.mp4` | Gazebo World Launch | [▶ Watch](#) |
| 2 | `2_Hexapod_teleop_node_sim.mp4` | Teleoperation | [▶ Watch](#) |
| 3 | `3_Hexapod_sensors_compute_sim.mp4` | Sensor Computation Layer | [▶ Watch](#) |
| 4 | `4_Hexapod_follower_sim.mp4` | Vision-Based Follower (YOLO) | [▶ Watch](#) |
| 5 | `5_Hexapod_swarm_follower_sim.mp4` | Swarm Follower | [▶ Watch](#) |
| 6 | `6_Hexapod_gps_navigation_sim.mp4` | Autonomous GPS Navigation | [▶ Watch](#) |
| 7 | `7_Hexapod_social_robot_launch_sim.mp4` | Social Robot — Hand Gestures | [▶ Watch](#) |

---

## 🤖 Real Robot Demonstrations — 9 Videos

> 📁 [`Real Robot Demonstrations/`](Real%20Robot%20Demonstrations/README.md)  
> 🎬 YouTube Playlist: **Hexapod Project — Real Robot (Raspberry Pi + Arduino)**

The same behaviors running on physical hardware: Raspberry Pi 4 + Arduino Mega + 18 servo motors. Real sensors, real noise, real consequences.

| # | Video File | Mode | YouTube |
|---|---|---|---|
| 1 | `1_Hexapod_dds_comunication_launch.mp4` | DDS Communication Launch | [▶ Watch](#) |
| 2 | `2_Hexapod_teleop_node.mp4` | Teleoperation | [▶ Watch](#) |
| 3 | `3_Hexapod_autobalance_node.mp4` | Auto-Balance Controller | [▶ Watch](#) |
| 4 | `4_Hexapod_compute_sensors_launch.mp4` | Sensor Computation Layer | [▶ Watch](#) |
| 5 | `5_Hexapod_follower_launch.mp4` | Vision Follower Launch | [▶ Watch](#) |
| 6 | `6_Hexapod_swarm_follower_launch.mp4` | Swarm Follower Launch | [▶ Watch](#) |
| 7 | `7_Hexapod_gps_navigation_launch.mp4` | GPS Navigation Launch | [▶ Watch](#) |
| 8 | `8_Hexapod_follower_demonstration.mp4` | Follower — Full Demo | [▶ Watch](#) |
| 9 | `9_Hexapod_gps_navigation_demonstration.mp4` | GPS Navigation — Full Demo | [▶ Watch](#) |

---

## 🔗 YouTube Playlists

| Playlist | Description |
|---|---|
| [🎮 Simulation (Gazebo + ROS2)](#-add-playlist-link-here) | 7 videos — full simulation pipeline |
| [🤖 Real Robot (Raspberry Pi + Arduino)](#-add-playlist-link-here) | 9 videos — physical hardware demos |

---

## 🧠 Operation Modes Demonstrated

| Mode | Simulation | Real Robot | Description |
|---|---|---|---|
| 🚀 **Gazebo Launch** | ✅ | — | Spawn robot and initialize physics + ROS2 bridge |
| 🕹️ **Teleoperation** | ✅ | ✅ | Manual keyboard control |
| ⚖️ **Auto-Balance** | — | ✅ | IMU-based postural stabilization |
| 📡 **Sensor Layer** | ✅ | ✅ | GPS, IMU, ultrasonic processing pipeline |
| 👁️ **Follower** | ✅ | ✅ | YOLO-based visual target tracking and pursuit |
| 🐝 **Swarm Follower** | ✅ | ✅ | Multi-agent coordination follower behavior |
| 🗺️ **GPS Navigation** | ✅ | ✅ | Autonomous goal-reaching with obstacle avoidance |
| 🖐️ **Social Robot** | ✅ | — | Hand gesture recognition → robot motion |

---

## 🛠️ Tech Stack

```
ROS2 Jazzy  ·  Gazebo Harmonic  ·  YOLO (Ultralytics)  ·  MediaPipe
Raspberry Pi 4  ·  Arduino Mega  ·  GPS  ·  IMU  ·  Ultrasonic
```

> 📦 Full source code: [github.com/Spin7/Hexapod-Project](https://github.com/Spin7/Hexapod-Project)
