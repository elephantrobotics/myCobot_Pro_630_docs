# Introduction to Phoenix API

**Note**: Phoenix API can only be run on the robot's main control, not on the customer's computer. If you want to use Phoenix API, you need to manually shut down Roboflow, otherwise an error will be reported

## Introduction to API interface
## 1 State management
### start_power_on_only()

- **Function:** The robot is only powered on, not enabled, and the Atom light at the end is on
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Power-on completed
- `False`: Power-on failed

### start_power_on_only()

- **Function:** The robot is only powered on, not enabled, and the Atom light at the end is on
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Power-on completed
- `False`: Power-on failed

### is_power_on()

- **Function:** Check if the robot is powered on
- **Parameters:** None
- **Return:**`(bool)`
- `True`: The robot is powered on
- `False`: The robot is not powered on

### is_servo_enabled(joint)

- **Function:** Get the corresponding joint connection status
- **Parameters:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:**`(bool)`
- `True`: Connected
- `False`: Not connected

### is_all_servos_enabled()

- **Function:** Get the connection status of all joints
- **Parameters:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:**`(bool)`
- `True`: All joints are connected
- `False`: There are unconnected joints/all joints are not connected

### start_robot()

- **Function:** The robot is powered on and enabled, and the Atom light at the end is on
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Startup completed
- `False`: Startup failed

### state_check()

- **Function:** Get system startup status
- **Parameter:** None
- **Return:**`(bool)`
- `True`: System started
- `False`: System not started

### check_running()

- **Function:** Get system startup status
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Moving
- `False`: Still

### set_free_move_mode(on=True)

- **Function:** Set free move mode
- **Parameter:**
- `True`: Turn on free move mode
- `False`: Turn off free move mode
- **Return:**`(bool)`
- `True`: Successfully turn on/off free movement mode
- `False`: Failed to turn on/off free movement mode

### is_software_free_move()

- **Function:** Determine whether free movement mode is turned on
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Free movement mode is turned on
- `False`: Free movement mode is not turned on

### get_payload()

- **Function:** Read robot arm payload
- **Parameter:** None
- **Return:**`(float)` Payload

### is_program_paused()

- **Function:** Determine whether the program is paused
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Program is paused
- `False`: Program is not paused

### get_error()

- **Function:** Read robot arm error information
- **Parameter:** None
- **Return:**`(tuple)` Return error information

### get_joint_min_pos_limit(joint)

- **Function:** Get the corresponding joint minimum angle
- **Parameter:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:**`(float)` Corresponding minimum joint angle

### get_joint_max_pos_limit(joint)

- **Function:** Get the corresponding joint maximum angle
- **Parameter:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:**`(float)` Corresponding maximum joint angle

### get_joint_max_pos_limit(joint)

- **Function:** Get the corresponding joint maximum angle
- **Parameter:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:**`(float)` Corresponding maximum joint angle

### get_acceleration()

- **Function:** Get robot arm acceleration
- **Parameter:** None
- **Return:** `(float)` Acceleration

### set_task_mode(task_mode)

- **Function:** Set robot task mode
- **Parameter:**
- `task_mode`: There are AUTO mode, MANUAL mode, MDI mode
- **Return:** `(bool)` Whether the task mode is set successfully (the return value is always true)

### release_joint_brake(joint, release=True)

- **Function:** Set joint brake status
- **Parameter:**
- `joint`: Joint.J1 ~ Joint.J6
- `release (bool)`: True - open brake False - close brake
- **Return:** None

### set_mdi_mode()

- **Function:** Set the working mode to MDI
- **Parameters:** None
- **Return:** None

### is_mdi_mode()

- **Function:** Determine whether the current working mode is MDI
- **Parameters:** None
- **Return:** `(bool)`
- `True`: MDI mode
- `False`: Not MDI mode

### is_manual_ok()

- **Function:** Confirm that the robot is in STATE_ON state and the robot is not currently running any instructions
- **Parameters:** None
- **Return:** `(bool)`
- `True`: The robot is in STATE_ON state and the robot is not currently running any instructions
- `False`: The instruction is not running/or is not in the disabled state





### get_motion_line()

- **Function:** Get the command line number currently being executed

- **Parameter:** None

- **Return:** The command line number currently being executed

### get_robot_status()

- **Function:** Get the robot arm status

- **Parameter:** None

- **Return:** `(bool)`

- `True`: Normal

- `False`: Closed/Error/Unable to move

### get_robot_temperature()

- **Function:** Get the robot arm CPU temperature

- **Parameter:** None

- **Return:** `(float)`: System temperature

### get_joint_state(joint)

- **Function:** Get the corresponding joint status

- **Parameter:**

- `joint`: Joint.J1 ~ Joint.J6

- **Return:** JointState

- `ERROR`: Joint error

- `OK`: Power on and enabled
- `ERROR`: POWERED_OFF

### get_joint_communication(joint)

- **Function:** Get the corresponding joint communication status
- **Parameter:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:** `(bool)`
- `True`: Communication is normal
- `False`: Communication failed

### set_power_limit(power_limit)

- **Function:** Set the robot power limit
- **Parameter:**
- `power_limit (float)`: Power limit
- **Return:** None

### get_power_limit()

- **Function:** Get the robot power limit
- **Parameter:** None
- **Return:**
- `float`: Power limit

### set_stopping_time(stopping_time)

- **Function:** Set the robot stop time
- **Parameter:**
- `stopping_time (float):`Stop time
- **Return:** None

### get_stopping_time()

- **Function:** Get robot arm stop time
- **Parameter:** None
- **Return:**
- `float`: Stop time

### set_stopping_distance(stopping_distance)

- **Function:** Set the current stop distance of the robot arm
- **Parameter:**
- `stopping_distance (float):`Stop distance
- **Return:** None

### get_stopping_distance()

- **Function:** Get the current stop distance of the robot arm
- **Parameter:** None
- **Return:**
- `float`: Stop distance

### set_tool_speed(tool_speed)

- **Function:** Get tool speed
- **Parameter:**
- `tool_speed (float):`Tool speed
- **Return:** None

### get_tool_speed()

- **Function:** Get the current stop distance of the robot

- **Parameter:** None

- **Return:**
- `float`: Tool speed

### set_tool_force(tool_force)

- **Function:** Set tool force

- **Parameter:**
- `tool_force (float):` Tool force

- **Return:** None

### get_tool_force()

- **Function:** Get tool force

- **Parameter:** None
- **Return:**
- `float`: Tool force

### set_max_speed(speed)

- **Function:** Get tool force

- **Parameter:**
- `speed:` Maximum speed, 0 ~ 100

- **Return:** None

### program_open(program_file_path)

- **Function:** Open G-code file, only supports absolute path

- **Parameter:**
- `program_file_path:` Absolute path of ngc file
- **Return:** None

### program_run(start_line)

- **Function:** Run G-code file from given line
- **Parameter:**
- `start_line (int):` Start line (first line is 0)
- **Return:**`(bool)`
- `True`: Send successfully
- `False`: Send failed

### get_current_line()

- **Function:** Run G-code file from given line
- **Parameter:** None
- **Return:**`int:` Current execution line
- `-1`: Program is not currently executed/execution is completed
- `1, 2, 3....x`: Program current execution line

### program_pause()

- **Function:** Pause program execution
- **Parameter:** None
- **Return:** None

### program_resume()

- **Function:** Resume program running
- **Parameters:** None
- **Return:** None

### task_stop()

- **Function:** Stop the robot and wait for the stop to complete
- **Parameters:** None
- **Return:** None

### get_digital_in(pin_number)

- **Function:** Get the value of the digital input pin
- **Parameters:**
- `pin_number (DI):` Input pin number
- **Return:**`(int)`
- `0`: No input
- `1`: Input

### get_digital_out(pin_number)

- **Function:** Get the value of the digital output pin
- **Parameters:**
- `pin_number (DO):` Output pin number
- **Return:**`(int)`
- `0`: No output
- `1`: Output

### set_digital_out(pin_number, pin_value)

- **Function:** Set the value of the digital output pin
- **Parameters:**
- `pin_number (DO)`: output pin number
- `pin_value (int)`: pin value (0 or 1)
- `0`: turn off output
- `1`: turn on output
- **Return:** None

### get_axis_speed(axis)

- **Function:** Get the corresponding axis speed
- **Parameters:**
- `axis`: Axis.X ~ Axis.RZ
- **Return:**
- `（float:）`: axis speed

### get_cmd_pos()

- **Function:** Get trajectory posture
- **Parameters:** None
- **Return:**
- `list[float]`: G-code string list

### get_cmd_joint()

- **Function:** Get the required joint angle
- **Parameters:** None
- **Return:**
- `list[float]`: [J1,J2,J3,J4,J5,J6]

### get_current_speed()

- **Function:** Get the current speed

- **Parameter:** None

- **Return:**
- `(float)`: Current speed

### get_default_speed()

- **Function:** Get the default speed

- **Parameter:** None

- **Return:**
- `(float)`: Default speed

### get_default_acceleration()

- **Function:** Get the default acceleration

- **Parameter:** None

- **Return:**
- `(float)`: Default acceleration

### get_max_speed()

- **Function:** Get the maximum speed

- **Parameter:** None

- **Return:**
- `(float)`: Maximum speed

### get_max_acceleration()

- **Function:** Get the maximum acceleration
- **Parameters:** None
- **Return:**
- `（float）`: Maximum acceleration

### get_feedrate()

- **Function:** Get the current feed rate
- **Parameters:** None
- **Return:**
- `（float）`: Current feed rate

### get_motion_enabled()

- **Function:** Get the status of the trajectory planner enable flag
- **Parameters:** None
- **Return:** `(bool)`
- `True`: Can move
- `False`: Cannot move

### coords_to_gcode(coords)

- **Function:** Convert the input coordinates to a G-code string
- **Parameters:**
- `coords(list[float | str])`: Coordinates
- **Return:** `list[str]` G-code

### angles_to_gcode(angles)

- **Function:** Convert the input angles to G-code string
- **Parameters:**
- `angles(list[float | str])`: angles
- **Return:** `list[str]` G-code

### coords_equal(coords_1, coords_2)

- **Function:** Determine whether the input coordinates are equal
- **Parameters:**
- `coords_1`: coordinates
- `coords_2`: coordinates
- **Return:** `(bool)`
- `True`: equal
- `False`: not equal

### cangles_equal(angles_1, angles_2)

- **Function:** Determine whether the input angles are equal
- **Parameters:**
- `angles_1`: angles
- `angles_2`: angles
- **Return:** `(bool)`
- `True`: equal
- `False`: not equal

### tool_get_firmware_version()

- **Function:** Get Pico firmware version number

- **Parameter:** None

- **Return:** Current firmware version

### tool_set_digital_out(pin_no, pin_value)

- **Function:** Set digital output pin value (end)

- **Parameter:**
- `pin_number (DO)`: output pin number
- `pin_value (int)`: pin value (0 or 1)
- `0`: turn off output
- `1`: turn on output
- **Return:** None

### tool_get_digital_in(pin_no)

- **Function:** Get digital input pin value (end)

- **Parameter:**
- `pin_no (int):` input pin number
- **Return:** `(int)`
- `0`: no input
- `1`: input

### tool_is_btn_clicked()

- **Function:** Determine whether the robot ATOM button is pressed
- **Parameter:** None
- **Return:** `(bool)`
- `True`: Pressed
- `False`: Not pressed

### tool_set_gripper_mode(mode)

- **Function:** Set the gripper mode
- **Parameter:**
- `mode:` Gripper mode
- `0`: 485 mode
- **Return:** None

### tool_set_gripper_enabled(enabled)

- **Function:** Set the gripper enable
- **Parameter:**
- `enabled:` Gripper mode
- `0`: Gripper release
- `1`: Gripper lock
- **Return:** None

### tool_set_gripper_calibrate()

- **Function:** Set the gripper calibration
- **Parameter:** None
- **Return:** None

### tool_set_gripper_value（value, speed）

- **Function:** Set the gripper angle
- **Parameter:**
- `value:` Gripper angle 0-100
- `speed:` Gripper speed 1-100
- **Return:** None

### tool_set_gripper_state(state, speed)

- **Function:** Set gripper enable
- **Parameter:**
- `state:` Gripper state
- `0`: Fully open
- `1`: Fully closed
- `speed:` Gripper speed 1-100
- **Return:** None

### clear_all_errors()

- **Function:** Clear all errors
- **Parameter:** None
- **Return:** None

### recover_robot()

- **Function:** Recover after collision or other errors are detected
- **Parameter:** None
- **Return:** `(bool)`
- `True`: Recovery successful
- `False`: Recovery failed

### enable_manual_brake_control()

- **Function:** Enable or disable manual brake control.
- **Parameters:** None
- **Return:** None

### set_joint_torque_limit(joint, torque_limit)

- **Function:** Set Cartesian torque limit
- **Parameters:**
- `joint:` Axis.X ~ Axis.RZ
- `torque_limit(float):` Torque limit value
- **Return:** None

### set_axis_torque_limit(axis, value)

- **Function:** Set the corresponding joint torque limit value
- **Parameters:**
- `axis:` Joint.J1 ~ Joint.J6
- `torque_limit(float):` Torque limit value
- **Return:** None

## 2 Motion Management

### get_coords()

- **Function:** Get all coordinates
- **Parameters:** None
- **Return:** `(list)`
- `[X,Y,Z,RX,RY,RZ]`

### get_coord(axis)

- **Function:** Get the corresponding coordinates
- **Parameters:**
- `axis`: Axis.X ~ Axis.RZ
- **Return:** Coordinates

### get_angles()

- **Function:** Get all joint angles
- **Parameters:** None
- **Return:**`(list)`
- `[J1,J2,J3,J4,J5,J6]`

### get_angle(joint)

- **Function:** Get the corresponding joint angles
- **Parameters:**
- `joint`: Joint.J1 ~ Joint.J6
- **Return:** Joint angles

### set_coords(list, speed)

- **Function:** Control multi-coordinate motion
- **Parameters:**
- `list`: [X,Y,Z,RX,RY,RZ]
- `speed`: 0~100
- **Return:** None

### set_coord(axis, coord, speed)

- **Function:** Control single coordinate motion
- **Parameter:**
- `axis:`: Axis.X ~ Axis.RZ
- `coord`: Coordinate
- `speed`: 0-100
- **Return:** None

### set_angles(list, speed)

- **Function:** Control multi-joint motion
- **Parameter:**
- `list`: [J1,J2,J3,J4,J5,J6]
- `speed`: 0~100
- **Return:** None

### set_angle(joint, angle, speed)

- **Function:** Control single joint motion
- **Parameter:**
- `joint:`: Joint.J1 ~ Joint.J6
- `angle`: angle
- `speed`: 0-100
- **Return:** None

### is_in_position(coords, is_linear)

- **Function:** Determine whether the robot arm moves to the corresponding angle/coordinate
- **Parameter:**
- `coords (list[float])`: coordinate/angle
- `is_linear (bool)`:
- False (0) - angle
- True (1) - coordinate
- **Return:** `(bool)`
- `True`: Movement is in place
- `False`: Movement is not in place

### is_in_commanded_position()

- **Function:** Determine whether the robot arm moves to the corresponding angle/coordinate
- **Parameter:** None
- **Return:** `(bool)`
- `True`: Movement is in place
- `False`: Movement is not in place

### jog_absolute_coord(axis, coord, speed)

- **Function:** Control single coordinate continuous motion
- **Parameter:**
- `axis`: Axis.X ~ Axis.RZ
- `coord (float)`: coordinate
- `speed (float)`: 0~100
- **Return:**`(bool)`
- `True`: Start continuous operation
- `False`: Failure

### jog_stop_all()

- **Function:** Stop all angle/coordinate motions
- **Parameter:** None
- **Return:**`(bool)`
- `True`: Stop successfully