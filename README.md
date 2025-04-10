![labview heating logo](./pictures/labview-heating-logo.png)

# scada-labview-heating-control-system

SCADA Heating Control System using LabVIEW Datalogging and Supervisory Control Module

## State Transition Table

| STATES                                        | Trigger/Action Description                  |
|-----------------------------------------------|---------------------------------------------|
| Idle – Standby (Power on/off)                 | Toggle power to enter standby mode          |
| Heating element on – heating up               | Activate heating element (start heating)    |
| Heating element off – cooling down            | Deactivate heating element (begin cooling)  |
| Manual mode (manual control switch enabled)   | Enable manual control via switch            |
| Automatic Mode                                | Engage automatic control routine            |
| Error condition – maintenance mode            | Detect system error; enter maintenance mode |


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