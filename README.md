![labview heating logo](./pictures/labview-heating-logo.png)

# scada-labview-heating-control-system

SCADA Heating Control System using LabVIEW Datalogging and Supervisory Control Module

## State Table

| State Name              | Description                                                                 | Entry Action                     | Exit Action                      |
|-------------------------|-----------------------------------------------------------------------------|----------------------------------|----------------------------------|
| Idle (Standby)          | System inactive, waiting for triggers.                                      | Turn off heating element.        | Prepare for heating/cooling.     |
| Heating Element On      | Actively heating to reach target temperature.                               | Enable heating element.          | Disable heating element.         |
| Heating Element Off     | Cooldown phase (prevents rapid cycling).                                    | Start cooldown timer.            | Reset timer.                     |
| Manual Mode             | User overrides automatic control.                                           | Disable automatic transitions.   | Re-enable automatic logic.       |
| - Manual Heating On     | User forces heating element on.                                             | Enable heating element.          | –                                |
| - Manual Heating Off    | User forces heating element off.                                            | Disable heating element.         | –                                |
| Error Condition         | Activated on critical faults (e.g., sensor failure).                        | Trigger alarms, log errors.      | Reset faults after maintenance.  |




## State Transition tables

#### Automatic Mode Transitions
| From State          | To State              | Trigger/Condition                                                                 |
|---------------------|-----------------------|-----------------------------------------------------------------------------------|
| Idle                | Heating Element On    | Temperature < Setpoint (auto mode enabled).                                       |
| Heating Element On  | Heating Element Off   | Temperature ≥ Setpoint OR heating timer expires.                                  |
| Heating Element Off | Idle                  | Cooldown timer expires OR temperature stabilizes.                                |
| Heating Element Off | Heating Element On    | Temperature < Setpoint again (before cooldown completes).                         |

#### Manual Mode Transitions
| From State              | To State              | Trigger/Condition                                                                 |
|-------------------------|-----------------------|-----------------------------------------------------------------------------------|
| Any state              | Manual Mode           | Manual control switch enabled.                                                   |
| Manual Mode (Heating On)| Manual Mode (Off)     | User toggles manual switch to "Off".                                              |
| Manual Mode (Heating Off)| Manual Mode (On)     | User toggles manual switch to "On".                                               |
| Manual Mode            | Idle                  | Manual control switch disabled.                                                   |

#### Error Handling
| From State              | To State              | Trigger/Condition                                                                 |
|-------------------------|-----------------------|-----------------------------------------------------------------------------------|
| Any state              | Error Condition       | Critical fault detected (e.g. sensor failure, temperature over 100°C).                                   |
| Error Condition         | Idle                  | Maintenance complete + system reset.                                              |




## Block Diagram

### Idle State:  

![](./pictures/block-diagram-idle-case.png)

### Filling State:  

![](./pictures/block-diagram-filling-case.png)

### Emptying State:  

![](./pictures/block-diagram-emptying-case.png)

## Front Panel

### Controls and indicators: 

![](./pictures/front-panel.png)
