\# Traffic Light Controller using FSM in Verilog



\## Overview

This project implements a realistic traffic light controller using Finite State Machine (FSM) principles in Verilog HDL.  
The design closely models real-world traffic signal behavior by incorporating timing control, pedestrian handling, minimum green time enforcement, and emergency vehicle priority.
The controller is written using parameter-based state encoding (without enum) to ensure compatibility with standard Verilog tools such as Vivado and HDLBits.

---

\## Objectives

\- Design a traffic light controller using FSM concepts
\- Implement realistic timing behavior using counters
\- Handle pedestrian requests safely
\- Provide emergency vehicle priority
\- Follow industry-style, synthesizable Verilog coding practices

---


\## Features

\- Moore FSM-based traffic light controller
\- Parameterized state encoding (no enum)
\- Counter-based delay for each traffic signal
\- Different timing for RED, GREEN, and YELLOW
\- Minimum green time for vehicle safety
\- Pedestrian request button
\- WALK / DON’T WALK pedestrian signals
\- Emergency GREEN override
\- Fail-safe default behavior for invalid states



---



\## FSM Description



\### FSM Type

\- Moore Machine
\- Outputs depend only on the current state

\### FSM States

The controller operates with three states:
\- RED
\- GREEN
\- YELLOW

State transition sequence:

RED → GREEN → YELLOW → RED



---



\## State Encoding

States are encoded using Verilog parameters:

```verilog

parameter s_red    = 2'b00;

parameter s_green  = 2'b01;

parameter s_yellow = 2'b10;

```

\##Timing Control

-Realistic timing behavior is achieved using a counter-based approach.
-Each FSM state is held for a predefined duration
-The counter increments while the FSM remains in the same state
-The counter resets automatically on every state transition
Example timing configuration:

```

RED_TIME = 10 seconds

GREEN_TIME = 8 seconds

YELLOW_TIME = 2 seconds

```

This timing control models real traffic signal delays and ensures stable transitions.



\##Minimum Green Time

-To ensure safe traffic operation:
-The GREEN signal remains active for a minimum duration
-Pedestrian requests are ignored until the minimum green time is satisfied
-This prevents unsafe immediate transitions after vehicles begin moving.



\##Pedestrian Button Handling

-A pedestrian request button allows users to request a crossing:
-Requests are evaluated only after minimum green time
-FSM transitions follow: GREEN → YELLOW → RED
\-Pedestrians are allowed to cross during RED
\-The button requests a transition but does not force an immediate change.



\##WALK / DON’T WALK Signals

-Pedestrian signals are derived directly from vehicle signal states:
-WALK signal is active during RED
-DON’T WALK signal is active during GREEN, YELLOW, and emergency conditions
-No additional FSM states are introduced for pedestrian control.



\##Emergency Vehicle Priority

-An emergency input provides highest priority operation:
-Forces GREEN output immediately
-Overrides normal FSM output behavior
-FSM state and internal timing logic remain unchanged
-Normal operation resumes once the emergency signal is deasserted
-This ensures safe and predictable behavior during emergency scenarios.



\###Tools Used

-Verilog HDL
-Vivado Simulator



\###Author

Ritesh Kumar


