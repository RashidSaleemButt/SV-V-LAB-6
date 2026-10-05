# Task 2: Formalize Constraints - ARLCCS

## Variable Definitions

| Variable Name | Data Type | Description |
|---|---|---|
| TrainDetected | Boolean | TRUE if train is present in detection zone or on crossing; FALSE otherwise. |
| BarrierLowered | Boolean | TRUE if barrier is in fully lowered position (confirmed by position sensor); FALSE otherwise. |
| WarningLightsActive | Boolean | TRUE if warning lights are activated and functioning; FALSE otherwise. |
| WarningBellActive | Boolean | TRUE if warning bell/audio alarm is activated and functioning; FALSE otherwise. |
| SensorFault | Boolean | TRUE if any sensor component reports a malfunction; FALSE if all sensors operational. |
| CommunicationLoss | Boolean | TRUE if communication lost with any critical actuator; FALSE if all communications normal. |
| EmergencyStop | Boolean | TRUE if emergency stop button is pressed; FALSE otherwise. |
| BarrierDescentInProgress | Boolean | TRUE if barrier is currently descending; FALSE otherwise. |
| DescentTimeElapsed | Integer | Time in seconds since barrier descent command was issued. |
| DescentCompleted | Boolean | TRUE when barrier reaches full lowered position; FALSE otherwise. |
| SystemInSafeState | Boolean | TRUE if barrier is lowered and all warnings active; FALSE otherwise. |
| TrainDeparted | Integer | Time in seconds since train last detected on crossing. |

## Formalized Constraints

| Constraint ID | Description (Simple English) | Formal Logical Expression |
|---|---|---|
| C1 | If a train is detected, the barrier must be lowered within 2 seconds. | TrainDetected → (¬BarrierLowered → BarrierDescentInProgress) ∧ (DescentTimeElapsed ≤ 2 → DescentCompleted) |
| C2 | Barrier remains lowered while train is detected or in crossing. | TrainDetected → BarrierLowered |
| C3 | Barrier raises only after train departure and 5-second delay. | (¬TrainDetected ∧ TrainDeparted > 5) → (BarrierLowered → ¬BarrierDescentInProgress) |
| C4 | Warning lights activate at least 10 seconds before barrier descent. | TrainDetected → (WarningLightsActive ∧ (BarrierDescentInProgress → ¬DescentTimeElapsed ≥ 10)) |
| C5 | Warning bell activates with barrier descent and stays active until fully lowered. | BarrierDescentInProgress → (WarningBellActive ∧ (¬DescentCompleted → WarningBellActive)) |
| C6 | Sensor fault triggers safe-fail: lower barrier and activate all warnings. | SensorFault → (BarrierLowered ∧ WarningLightsActive ∧ WarningBellActive) |
| C7 | Communication loss triggers barrier descent and fail-safe warnings. | CommunicationLoss → (BarrierDescentInProgress ∧ WarningLightsActive ∧ WarningBellActive) |
| C8 | Emergency stop immediately lowers barrier and activates all warnings. | EmergencyStop → (BarrierDescentInProgress ∧ WarningLightsActive ∧ WarningBellActive ∧ SystemInSafeState) |
