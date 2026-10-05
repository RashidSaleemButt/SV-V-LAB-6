# Task 1: Identify Constraints - ARLCCS

| Constraint ID | Constraint (Simple English) | Reason / Necessity |
|---|---|---|
| C1 | If a train is detected in the crossing zone, the barrier must begin lowering immediately. | Safety requirement to block vehicle access when a train is present. |
| C2 | The barrier must remain fully lowered while a train occupies the crossing zone or is actively crossing. | Critical safety measure to prevent vehicle-rail collisions. |
| C3 | The barrier can only begin raising after the train has completely departed and a minimum 5-second safety delay has elapsed. | Ensures train is fully clear before permitting road traffic; prevents premature barrier opening. |
| C4 | Warning lights must activate at least 10 seconds before the barrier begins descending. | Provides adequate alert time for drivers and pedestrians to stop or clear the crossing. |
| C5 | The warning bell/audio alarm must remain active throughout barrier descent and until the barrier is fully lowered. | Ensures continuous audible warning for vision-impaired and inattentive road users. |
| C6 | If any sensor component malfunctions, the system must immediately enter fail-safe mode: lower the barrier and activate all warning signals. | Prevents undetected sensor failures from compromising safety. |
| C7 | If communication is lost with any critical actuator (barrier motor, light controller, bell controller), the system must immediately lower the barrier and activate all warnings. | Prevents loss of control from leaving the crossing unprotected. |
| C8 | An emergency stop button press must immediately trigger barrier descent and activate all warning systems, regardless of other system states. | Allows manual override for emergency situations. |
| C9 | The barrier position sensor must be continuously monitored; if it reports an invalid state (e.g., neither raised nor lowered), the system must fail-safe. | Ensures barrier position accuracy; detects mechanical or sensor faults. |
| C10 | No vehicle or pedestrian detection system shall be used to override or prevent barrier lowering once a train is detected. | Prevents logic errors from causing barrier to remain raised when occupied. |
