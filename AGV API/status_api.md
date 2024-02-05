<H1> Status API </H1>

---
<!-- TOC -->
  * [Robot status](#robot-status)
      * [PGVs](#pgvs)
      * [IOs](#ios)
      * [Msg](#msg)
<!-- TOC -->

---

## Robot status
<H3> Request </H3>

Code:           3000 

Description:    Read robot data request 

JSON data:      *N/A*

<H3> Response </H3>
Code:           13000

Description:    Read robot data response

JSON data:      *table below*

| Key             | Data type     | Description                                                                          |
|:----------------|---------------|--------------------------------------------------------------------------------------|
| x               | float         | x coordinate of robot (m)                                                            |
| y               | float         | y coordinate of robot (m)                                                            |
| angle           | float         | angle of robot (°)                                                                   |
| vx              | float         | x velocity of robot                                                                  |
| vy              | float         | y velocity of robot                                                                  |
| w               | float         | angular velocity of robot                                                            |
| spin            | float         | turntable angle                                                                      |
| pgvs            | [PGVs](#pgvs) | PGV data                                                                             |
| target_id       | int           | the current navigation destination layout node ID                                    |
| finished_path   | list[int]     | list of layout node ID for completed node during navigation                          |
| unfinished_path | list[int]     | list of layout node ID for incomplete node during navigation                         |
| task_status     | int           | 0: Idle<br/>1: Running<br/>2: Completed<br/>3: Paused<br/>4: Cancelled<br/>5: Failed |
| battery_level   | float         | current battery level (%)                                                            |
| voltage         | float         | current battery voltage (V)                                                          |
| current         | float         | current battery current (A)                                                          |
| charging        | bool          | robot in charging state                                                              |
| io_status       | [IOs](#ios)   | list of IO status dictionary data                                                    |
| fatals          | [Msg](#msg)   | list of msg dictionary data for fatal messages                                       |
| errors          | [Msg](#msg)   | list of msg dictionary data for error messages                                       |
| warnings        | [Msg](#msg)   | list of msg dictionary data for warning messages                                     |
| odo             | float         | total odometry data (m)                                                              |
| today_odo       | float         | today total odometry data (m)                                                        |
| time            | float         | total online time (hr)                                                               |
| total_time      | float         | today total online time (hr)                                                         |
| emergency       | bool          | emergency push button is pushed                                                      |
| soft_emc        | bool          | emergency triggered via software                                                     |
| is_stopped      | bool          | robot is stationary                                                                  |
| is_slowed       | bool          | robot is slowed due to obstacle detection                                            |
| is_blocked      | bool          | robot is stopped due to obstacle detection                                           |
| reloc_status    | int           | 0: Not relocated<br/>1: Relocation completed<br/>2: Relocation failed                |
| rssi            | float         | the wireless communication strength (%)                                              |

---

#### PGVs
```json
{
  "pgvs": [
    {
      "pgv_id": 0,
      "tag_value": 100, 
      "tag_dif_x": 10.2, 
      "tag_dif_y": 5.7,
      "tag_dif_angle": 1.234
    },
    {
      "pgv_id": 1,
      "tag_value": 120, 
      "tag_dif_x": 8.7, 
      "tag_dif_y": 3.1,
      "tag_dif_angle": 0.123
    }
  ]
}
```

#### IOs
```json
{
  "io_status": {
    "di": [
      {"0": true},
      {"1": false},
      {"2": false},
      {"3": false},
      {"4": false},
      {"5": false},
      {"6": true},
      {"7": false}
    ],
    "do": [
      {"0": false},
      {"1": true},
      {"2": true},
      {"3": false},
      {"4": false},
      {"5": false},
      {"6": false},
      {"7": true}      
    ]
  }
}
```

#### Msg
```json
{
  "fatals": [
    {
      "code": 1219,
      "time_occurred": "26/01/2024 16:24:11.290",
      "description": "drive 1 motor overload"
    },
    {
      "code": 1112,
      "time_occurred": "26/01/2024 16:27:45.290",
      "description": "controller SD card faulty"
    }
  ],
  "errors": [
    {
      "code": 2001,
      "time_occurred": "26/01/2024 16:24:11.290",
      "description": "tag is not detected after moving some distance"
    },
    {
      "code": 2009,
      "time_occurred": "28/01/2024 12:41:35.178",
      "description": "jacking run time over"
    }
  ],
  "warnings": [
    {
      "code": 3003,
      "time_occurred": "28/01/2024 12:41:35.178",
      "description": "battery communication lost"
    }    
  ]
}
```