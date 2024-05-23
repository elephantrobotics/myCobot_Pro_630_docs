# phoenix module

### _class_ phoenix.Phoenix(debug=False)

Bases: `object`

Interface for Phoenix - robot controller.

Methods starting with underscore (‘\_’) are low level and not intended to be
used by users of this class.

### Example

- Start / Stop Robot Workflow:
  1. start_robot() or start_power_on_only()
  2. …
  3. shutdown_robot()
  4. go to 1.

#### angles_to_gcode(angles)

Returns gcode string to move to given joint angles

- **Parameters:**
  **coords** (_list_ _[\*\*float_ _|_ _str_ _]_) – list of joint angles values
- **Returns:**
  gcode string to move to given joint angles
- **Return type:**
  str

#### apply_hal_config()

Runs halcmd and applies elerob_gpio.hal config.



#### coords_equal(coords_1, coords_2)

Checks if specified coords are equal.

- **Parameters:**
  - **coords_1** (_list_) – first coords to compare
  - **coords_2** (_list_) – second coords to compare
- **Returns:**
  True if coords are equal, False otherwise.
- **Return type:**
  bool

#### coords_to_gcode(coords)

Returns gcode string to move to given coords

- **Parameters:**
  **coords** (_list_ _[\*\*float_ _|_ _str_ _]_) – list of coordinate values
- **Returns:**
  gcode string to move to given coords
- **Return type:**
  str

#### detect_robot()

Detects robot from Analog Input HAL pin.



#### ensure_mdi()

Sets mode to MDI.

#### ensure_mode(m, \*p)

If elerob is not already in one of the model given, switch it to
the first mode: elerob.MODE_MDI, elerob.MODE_MANUAL, elerob.MODE_AUTO.

- **Parameters:**
  **m** ([_TaskMode_](#phoenix.TaskMode)) – TaskMode or “STEP_MODE” (same as TaskMode.MDI)
- **Returns:**
  True if mode is m or in p
- **Return type:**
  bool

#### float_equal(a, b, epsilon=0.5)

Compares 2 floats with given epsilon precision.

- **Parameters:**
  - **a** (_float_) – 1st float to compare
  - **b** (_float_) – 2nd float to compare
  - **epsilon** (_float_) – precision (epsilon) to compare
- **Returns:**
  True if floats are considered equal with given precision,
  : False otherwise
- **Return type:**
  bool








#### get_angles()

Returns robot’s current joint angle values.

- **Returns:**
  current angles list[float] of size MAX_JOINTS
- **Return type:**
  list[float]





#### get_cmd_joint_float()

Returns desired joint positions.

- **Returns:**
  list of string of values
- **Return type:**
  list[float]

#### get_cmd_pos_float()

Returns commanded robot’s position.

- **Returns:**
  list of strings of values
- **Return type:**
  list[float]










































#### get_motion_enabled()

State of trajectory planner enabled flag.
True if robot can move, false otherwise.
轨迹规划器启用标志的状态。如果机器人可以移动，则为 True，否则为 False

- **Returns:**
  enabled flag value
- **Return type:**
  bool











#### get_robot_status()

Returns robot status.

- **Returns:**
  True if OK, False if disabled / error / cannot move
- **Return type:**
  bool





#### get_stopping_distance()

Returns current stopping distance.

- **Returns:**
  stopping distance
- **Return type:**
  float

#### get_stopping_time()

Returns stopping time.

- **Returns:**
  stopping time
- **Return type:**
  float



#### get_tool_force()

Returns current tool force.

- **Returns:**
  tool force
- **Return type:**
  float



#### init_can()

Initializes CAN bus.

#### init_can_output(servo_id)

Init servo IO output.

- **Parameters:**
  **servo_id** ([_Joint_](#phoenix.Joint)) – one of Joint enum’s values

#### init_hal()

Initializes HAL (Hardware Abstraction Layer) of Phoenix.

#### init_hal_gpio()

Inits HAL pins and parameters in halgpio component.

#### init_hal_serial()

Initializez HAL parameters of serial component.

#### init_robot()

Initializes robot parameters.










































#### manual_ok(do_poll=True)

Returns True if robot state is elerob.STATE_ON and g-code interpreter
state is elerob.INTERP_IDLE.

- **Parameters:**
  **do_poll** (_bool_ _,_ _optional_) – Update robot data before checking state. Defaults to True.
- **Returns:**
  True if robot state is elerob.STATE_ON and g-code interpreter
  : state is elerob.INTERP_IDLE.
- **Return type:**
  bool











### Example

elerob.program_run(elerob.AUTO_RUN, 0)

- **Returns:**
  True if program run started successfully, False otherwise
- **Return type:**
  bool

#### receive_can(timeout=0.5)

Receives next message from CAN bus.

- **Parameters:**
  **timeout** (_float_ _,_ _optional_) – How long time to receive message. Defaults to 0.5.
- **Returns:**
  CAN message or None (if no message could be received).
- **Return type:**
  Message | None



#### send_can(data, can_id=7)

Sends CAN message.

- **Parameters:**
  - **data** (_list_ _[\*\*int_ _]_) – message bytes, e.g. [0xFE, 0x01]
  - **can_id** (_hexadecimal_ _,_ _optional_) – CAN ID. Defaults to 0x007.



#### send_mdi(gcode_command)

Send G-Code command to robot.

- **Parameters:**
  **gcode_command** (_str_) – G-code command
- **Returns:**
  True if command sent successfully, False otherwise
- **Return type:**
  bool

#### send_mdi_wait(gcode_command)

Send command and wait for it to complete.

- **Parameters:**
  **program** (_str_) – G-code command


























#### set_jog_mode(jog_mode)

Changes jog mode to jog_mode (angular or linear).
AKA jog_state_check().

- **Parameters:**
  **jog_mode** ([_JogMode_](#phoenix.JogMode)) – linear (JogMode.JOG_TELEOP) or
  angular (JogMode.JOG_JOINT) jog mode
- **Returns:**
  True if change state was successful, False otherwise
- **Return type:**
  bool









#### set_motion_flexible(flexible)

Sets motion flexible flag.

- **Parameters:**
  **flexible** (_bool_) – True / False

#### set_output(servo_id, state)

Sets servo IO state.

- **Parameters:**
  - **servo_id** ([_Joint_](#phoenix.Joint)) – one of Joint enum’s values
  - **state** (_int_) – 0 or 1







#### set_stopping_distance(stopping_distance)

Sets stopping distance.

- **Parameters:**
  **stopping_distance** (_float_) – stopping distance

#### set_stopping_time(stopping_time)

Sets stopping time.

- **Parameters:**
  **stopping_time** (_float_) – stopping time



#### set_teleop(enable)

Enables/disables teleop mode (cartesian movement by axes).

- **Parameters:**
  **enable** (_bool_) – True to enable (cartesian movement), False to disable (joint movement)








#### state_off()

Sets robot state to OFF.

#### state_on()

Sets robot state to ON.

- **Returns:**
  True if success, False otherwise.
- **Return type:**
  bool




























