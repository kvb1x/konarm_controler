# install moveit
https://moveit.picknik.ai/main/doc/tutorials/getting_started/getting_started.html

# create pacakge
ros2 pkg create --build-type ament_python --license Apache-2.0 --node-name controler_xyz  controler


---

## How to Run

To start the full simulation and control environment, you need to open **4 separate terminals**. 
*Note: Remember to source your ROS 2 workspace in each terminal using `source install/setup.bash` before running the commands.*

### Terminal 1: Launch Robot Model & RViz
Starts the robot state publisher, standard controllers, and the RViz2 visualization tool.
```bash
ros2 launch sdrac_moveit_config demo.launch.py
```



### Terminal 2: Launch MoveIt Servo
The main node responsible for real-time kinematics calculations based on the received commands.
```bash
ros2 launch controler run_servo.launch.py
```



### Terminal 3: Launch Remote 6D Communication Node
This node receives UDP data from the controller and translates it into motion commands.
```bash
ros2 launch remote_6d remote_servo_control.launch.py
```



### Terminal 4: 6D Controller Simulator
Runs the virtual keyboard controller that sends network packets to port 25000. You can switch between Konarm's Base reference frame and the Tool (end-effector) reference frame by pressing "1" on the keyboard.
```bash
python3 -m venv .venv
source .venv/bin/activate
python3 konarm/src/konarm_controler/src/Pilot_6_axis/keyboard_rc.py -i 127.0.0.1 -p 25000
```



![RViz Teleoperation Demo](images/demo_rviz.webp)

