<H1> Control API </H1>

---
<!-- TOC -->
  * [Clear all errors](#clear-all-errors)
  * [Relocation request](#relocation-request)
  * [Confirm relocation](#confirm-relocation)
  * [Pause task](#pause-task)
  * [Resume task](#resume-task)
  * [Cancel task](#cancel-task)
  * [Path navigation task](#path-navigation-task)
      * [nav_task](#navtask)
  * [Translation task](#translation-task)
  * [Rotation task](#rotation-task)
  * [Spinning task](#spinning-task)
  * [Jack up task](#jack-up-task)
  * [Jack down task](#jack-down-task)
  * [Homing task](#homing-task)
  * [Set DO](#set-do)
<!-- TOC -->

---


## Clear all errors
<H3> Request </H3>

Code:           2000 

Description:    Reset all the errors 

JSON data:      *N/A*

<H3> Response </H3>
Code:           12000

Description:    Reset errors response

JSON data:      *N/A*

---
## Relocation request
<H3> Request </H3>

Code:           2001 

Description:    Manually relocate the robot

JSON data:      *table below*

| Key   | Data type | Description        | Required | Default value |
|-------|-----------|--------------------|----------|---------------|
| x     | float     | Coordinate x (m)   | Yes      | -             |
| y     | float     | Coordinate y (m)   | Yes      | -             |
| angle | float     | Angle of robot (°) | Yes      | -             |

<H3> Response </H3>
Code:           12000

Description:    Manually relocation response

JSON data:      *N/A*

---
## Confirm relocation
<H3> Request </H3>

Code:           2002 

Description:    Confirm the current position of the robot

JSON data:      *N/A*

<H3> Response </H3>
Code:           12000

Description:    Confirm the current position response

JSON data:      *N/A*

---
## Pause task
<H3> Request </H3>

Code:           2003 

Description:    Pause the current task execution request

JSON data:      *N/A*

<H3> Response </H3>
Code:           12003

Description:    Pause the current task execution response

JSON data:      *N/A*

---
## Resume task
<H3> Request </H3>

Code:           2004 

Description:    Resume the current task execution request

JSON data:      *N/A*

<H3> Response </H3>
Code:           12004

Description:    Resume the current task execution response

JSON data:      *N/A*

---
## Cancel task
<H3> Request </H3>

Code:           2005 

Description:    Cancel the current task execution request

JSON data:      *N/A*

<H3> Response </H3>
Code:           12005

Description:    Cancel the current task execution response

JSON data:      *N/A*

---
## Path navigation task
<H3> Request </H3>

Code:           2006 

Description:    Send the path navigation task request. \
A path navigation is made up of a list of nav_task, in which each of the nav_task must be able to connect from predecessor layout node to successor layout node.

JSON data:      *table below*

| Key           | Data type                  | Description                        | Required | Default value |
|---------------|----------------------------|------------------------------------|----------|---------------|
| nav_task_list | list[[nav_task](#navtask)] | The path for the robot to navigate | Yes      | -             |

#### nav_task

```json
{
  "nav_task": {
      "task_id": "12001",
      "from_id": 102,
      "to_id": 112,
      "operation": "JackLoad",
      "adjust_down_pgv": true,
      "adjust_theta": 90.0
    }
}
```
Description of nav_task:

| Key             | Data type | Description                                                           | Required | Default value |
|-----------------|-----------|-----------------------------------------------------------------------|----------|---------------|
| task_id         | str       | Unique task id for each nav_task                                      | Yes      | -             |
| from_id         | int       | Predecessor barcode tag ID                                            | Yes      | -             |
| to_id           | int       | Successor barcode tag ID                                              | Yes      | -             |
| angle           | float     | The angle of robot upon reaching destination (°)                      | No       | -             |
| operation       | str       | The subsequent operation of robot upon reaching destination           | No       | -             |
| adjust_down_pgv | bool      | Secondary adjustment using down pgv                                   | No       | -             |
| adjust_theta    | float     | Secondary adjustment angle (°). Only valid if adjust_down_pgv is true | No       | 0             |

Task operations included:
* JackLoad
* JackUnload
* Spin

Sample below shows the JSON data for path navigation from 101 -> 102 -> 112, \
and with operation of JackLoad, adjust_down_pgv at 90° when robot arrives destination 120:
```json
{
  "nav_task_list": [
    {
      "task_id": "12000",
      "from_id": 101,
      "to_id": 102
    },
    {
      "task_id": "12001",
      "from_id": 102,
      "to_id": 112,
      "operation": "JackLoad",
      "adjust_down_pgv": true,
      "adjust_theta": 90.0
    }
  ]
}
```

<H3> Response </H3>
Code:           12006

Description:    Send the path navigation task response

JSON data:      *N/A*

---
## Translation task
<H3> Request </H3>

Code:           2007 

Description:    Send the translation task request

JSON data:      *table below*

| Key  | Data type | Description            | Required | Default value |
|------|-----------|------------------------|----------|---------------|
| dist | float     | Distance to travel (m) | Yes      | -             |
| v    | float     | Velocity (m/s)         | Yes      | -             |

<H3> Response </H3>
Code:           12007

Description:    Send the translation task response

JSON data:      *N/A*

---
## Rotation task
<H3> Request </H3>

Code:           2008 

Description:    Send the rotation task request. Theta is rotation relative to current angle. \
Angle is the absolute angle relative to the map. If both keywords are specified, angle will take effect only.

JSON data:      *table below*

| Key   | Data type | Description                    | Required | Default value |
|-------|-----------|--------------------------------|----------|---------------|
| theta | float     | Incremental rotation angle (°) | No       | -             |
| angle | float     | Absolute rotation angle (°)    | No       | -             |
| w     | float     | Angular velocity (m/s)         | Yes      | -             |

<H3> Response </H3>
Code:           12008

Description:    Send the rotation task response

JSON data:      *N/A*

---
## Spinning task
<H3> Request </H3>

Code:           2009 

Description:    Send the spinning task request

JSON data:      *table below*

| Key   | Data type | Description            | Required | Default value |
|-------|-----------|------------------------|----------|---------------|
| theta | float     | Rotation angle (°)     | Yes      | -             |
| w     | float     | Angular velocity (m/s) | Yes      | -             |

<H3> Response </H3>
Code:           12009

Description:    Send the spinning task response

JSON data:      *N/A*

---
## Jack up task
<H3> Request </H3>

Code:           2010 

Description:    Send the jack up task request. \
If the up limit sensor is activated, jack up will stop immediately even if the set stroke has not reached

JSON data:      *table below*

| Key    | Data type | Description             | Required | Default value |
|--------|-----------|-------------------------|----------|---------------|
| stroke | float     | The jacking stroke (mm) | Yes      | -             |

<H3> Response </H3>
Code:           12010

Description:    Send the jack up task response

JSON data:      *N/A*

---
## Jack down task
<H3> Request </H3>

Code:           2010 

Description:    Send the jack down task request

JSON data:      *N/A*

<H3> Response </H3>
Code:           12010

Description:    Send the jack down task response

JSON data:      *N/A*

---
## Homing task
<H3> Request </H3>

Code:           2011 

Description:    Send the homing task request. \
The robot will perform homing for its turntable and jacking mechanism.

JSON data:      *N/A*

<H3> Response </H3>
Code:           12011

Description:    Send the homing task response

JSON data:      *N/A*

---
## Set DO
<H3> Request </H3>

Code:           2012 

Description:    Set DO request

JSON data:      *table below*

| Key | Data type | Description              | Required | Default value |
|-----|-----------|--------------------------|----------|---------------|
| do  | int       | The digital output index | Yes      | -             |


<H3> Response </H3>
Code:           12012

Description:    Set DO response

JSON data:      *N/A*