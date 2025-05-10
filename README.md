![labview heating logo](./pictures/labview-heating-logo.png)

# scada-labview-heating-control-system

SCADA Heating Control System using LabVIEW Datalogging and Supervisory Control Module

## State Table

| State Name              | Description                                                                 | Entry Action                     | Exit Action                      |
|-------------------------|-----------------------------------------------------------------------------|----------------------------------|----------------------------------|
| Idle (Standby)          | System inactive, waiting for triggers.                                      | Turn off heating element.        | Prepare for heating/cool down.     |
| Automatic Heating Element On      | Actively heating to reach target temperature.                               | Enable heating element.          | Disable heating element.         |
| Automatic Heating Element Off     | Cooldown phase                                    |      Disable heating element.      |          Enable heating element.           |
| Manual Mode             | User overrides automatic control.                                           | Disable automatic transitions.   | Re-enable automatic logic.       |
| - Manual Heating On     | User forces heating element on.                                             | Enable heating element.          | –                                |
| - Manual Heating Off    | User forces heating element off.                                            | Disable heating element.         | –                                |
| Maintenance Mode         | Activated on critical faults (e.g., temperature over 100°C).                        | Temperature > 100°C     | Reset faults after maintenance.  |




## State Transition tables

#### Automatic Mode Transitions
| From State          | To State              | Trigger/Condition                                                                 |
|---------------------|-----------------------|-----------------------------------------------------------------------------------|
| Idle                | Heating Element On    | Temperature < Setpoint (auto mode enabled).                                       |
| Heating Element On  | Heating Element Off   | Temperature ≥ Setpoint                                 |
| Heating Element Off | Idle                  | Temperature stabilizes                                |
| Heating Element Off | Heating Element On    | Temperature < Setpoint                         |

#### Manual Mode Transitions
| From State              | To State              | Trigger/Condition                                                                 |
|-------------------------|-----------------------|-----------------------------------------------------------------------------------|
| Any state              | Manual Mode           | Manual control switch enabled.                                                   |
| Manual Mode (Heating On)| Manual Mode (Off)     | User toggles manual switch to "Off".                                              |
| Manual Mode (Heating Off)| Manual Mode (On)     | User toggles manual switch to "On".                                               |
| Manual Mode            | Idle                  | Manual control switch disabled.                                                   |

#### Maintenance Mode Transitions
| From State              | To State              | Trigger/Condition                                                                 |
|-------------------------|-----------------------|-----------------------------------------------------------------------------------|
| Any state              | Maintenance Mode       | Critical fault detected (e.g. temperature over 100°C).                                   |
| Maintenance Mode        | Idle                  | Maintenance complete + system reset.                                              |





## Server

### Front Panel

![](./pictures/server-front-panel.png)

### Block Diagram

#### Full Diagram:  

![](./pictures/server-block-diagram.png)

#### Initialization:  

![](./pictures/server-block-diagram-initialization.png)

#### Max and Min Temperature:  

![](./pictures/server-block-diagram-calculate-max-and-min-temp.png)

#### Track last 5 for Average:  

![](./pictures/server-block-diagram-track-last-5-for-average.png)

#### System Control State Management (Automatic):  

![](./pictures/server-block-diagram-system-control-state-management-automatic.png)

#### System Control State Management (Manual):  

![](./pictures/server-block-diagram-system-control-state-management-manual.png)

#### System Control State Management (Maintenance):  

![](./pictures/server-block-diagram-maintenance-state-management.png)

#### Password Control:  

![](./pictures/server-block-diagram-password-control.png)

#### Map Local Variables to Globals:  

![](./pictures/server-block-diagram-local-to-global.png)

#### Heating State Management (Heating ON):  

![](./pictures/server-block-diagram-heating-state-management-heating-on.png)

#### Heating State Management (Heating OFF):  

![](./pictures/server-block-diagram-heating-state-management-heating-off.png)

#### Logging to File:  

![](./pictures/server-block-diagram-file-output-1.png)
![](./pictures/server-block-diagram-file-output-2.png)
![](./pictures/historical-reading-output-csv.png)

## Client

### Front Panel

![](./pictures/client-front-panel.png)

### Block Diagram

![](./pictures/client-block-diagram.png)

## Global

### Front Panel

![](./pictures/global-front-panel.png)