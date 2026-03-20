# 🚗 Mobile Robot using URDF & Xacro

## 📌 Overview
This project defines a **mobile robot model** using both:
- **URDF (Unified Robot Description Format)**
- **Xacro (XML Macros for scalable robot design)**

It demonstrates how to build a robot structure with links, joints, and inertial properties, and how to simplify complex URDFs using reusable Xacro macros.

---

## 📂 Project Structure


my_first_pkg/
│── urdf/
│ ├── my_robot.urdf
│ ├── my_robot_using_xacro.urdf
│
│── CMakeLists.txt
│── package.xml
│── include/
│── src/


---

## ⚙️ Files Explanation

### 🔹 my_robot.urdf
- Pure URDF file
- Defines:
  - Robot links (base, legs, wheels, arms, head, gripper)
  - Fixed joints between components
  - Visual + collision geometry
- Includes:
  - Materials (color definitions)
  - Mesh-based gripper components

👉 Problem:  
URDF becomes **repetitive and hard to maintain** as complexity increases.

---

### 🔹 my_robot_using_xacro.urdf
- Uses **Xacro macros** for cleaner and reusable design
- Key features:
  - Parameterized dimensions (`base_width`, `base_length`, etc.)
  - Custom macro:
    ```xml
    <xacro:macro name="box_inertia">
    ```
  - Automatically computes inertia

👉 Advantage:
- Less duplication
- Easier scaling and modification
- Cleaner structure

👉 Reality check:
You are **not fully leveraging Xacro yet**.  
Left/right components are still manually duplicated instead of using reusable macros.

---

## 🧠 Robot Design Breakdown

### 🧱 Base
- Rectangular box structure
- Acts as main body

### 🦿 Legs & Base Extensions
- Left & Right legs attached to base
- Additional base links for wheel mounting

### ⚙️ Wheels
- Cylindrical geometry
- Fixed joints (not actuated yet)

👉 Issue:
All joints are `fixed`, so the robot **cannot move**

---

### 🤖 Upper Body
- Head (box or sphere)
- Arms (simple box structures)

### ✋ Gripper (URDF version only)
- Uses mesh files:
  - `l_finger.dae`
  - `l_finger_tip.dae`

👉 Problem:
These meshes depend on:

package://urdf_tutorial/

This will fail unless that package exists.

---

## 🚀 How to Run

### 1. Build workspace
```bash
colcon build
2. Source workspace
source install/setup.bash
3. Run URDF
ros2 run robot_state_publisher robot_state_publisher my_robot.urdf
4. Run Xacro version
ros2 run xacro xacro my_robot_using_xacro.urdf > robot.urdf
ros2 run robot_state_publisher robot_state_publisher robot.urdf
🧪 Visualization (RViz)
rviz2

Add:

RobotModel

TF

⚠️ Current Limitations

No actuated joints (all fixed)

No sensors (Lidar, Camera, etc.)

No Gazebo plugins

Xacro not fully optimized (still repetitive)

External mesh dependency may fail

🔥 Improvements (Next Steps)

Convert full structure into reusable Xacro macros

Change wheel joints to continuous for motion

Add Gazebo simulation support

Add sensors (Lidar, Camera)

Split Xacro into modular files:

materials.xacro

macros.xacro

robot.xacro

🧾 Tech Stack

ROS2

URDF

Xacro

RViz2

📌 Conclusion

This project is a solid beginner-to-intermediate step in robot modeling using ROS2.

Current state:

Works for visualization

Not suitable for real simulation or control

To make it production-level:

Add actuation

Author
Pratyush Vatsa

Add controllers

Add simulation
