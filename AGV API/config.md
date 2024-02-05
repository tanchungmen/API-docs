<H1> Config API </H1>

---
<!-- TOC -->
  * [Pushed data config](#pushed-data-config)
  * [Download parameters](#download-parameters)
  * [Upload parameters](#upload-parameters)
  * [Download map](#download-map)
      * [Layout](#layout)
  * [Upload map](#upload-map)
  * [Change map](#change-map)
  * [Delete map](#delete-map)
<!-- TOC -->

---

## Pushed data config
<H3> Request </H3>

Code:           1000 

Description:    Set pushed data config request

JSON data:      *table below*

| Key      | Data type | Description               | Required | Default value |
|----------|-----------|---------------------------|----------|---------------|
| interval | int       | Data pushed interval (ms) | No       | 500           |

<H3> Response </H3>
Code:           11000

Description:    Set pushed data config response

JSON data:      *N/A*

---

## Download parameters
<H3> Request </H3>

Code:           1001 

Description:    Download parameters request

JSON data:      *table below*

| Key | Data type | Description | Required | Default value |
|-----|-----------|-------------|----------|---------------|
| TBD | ...       | ...         | ...      | ...           |


<H3> Response </H3>
Code:           11001

Description:    Download parameters response

JSON data:      *N/A*

---

## Upload parameters
<H3> Request </H3>

Code:           1002 

Description:    Upload parameters request

JSON data:      *N/A*

<H3> Response </H3>
Code:           11002

Description:    Upload parameters response

JSON data:      *table below*

| Key | Data type | Description |
|:----|-----------|-------------|
| TBD | ...       | ...         |
---

## Download map
<H3> Request </H3>

Code:           1003 

Description:    Download map request

JSON data:      *table below*

| Key    | Data type         | Description                               | Required | Default value |
|--------|-------------------|-------------------------------------------|----------|---------------|
| layout | [Layout](#layout) | The layout data to be downloaded to robot | Yes      | -             |

#### Layout
Sample below shows the JSON data for layout. \
Nodes is list of nodes and each node is described as below. \
Paths is list of paths and each path is described as below.
```json
{
  "layout": {
    "layout_name": "AGV area GF",
    "total_x": 10.5,
    "total_y": 16.0,
    "x_node_dist": 1.2,
    "y_node_dist": 1.2,
    "nodes": [
      {
        "x": 1.5,
        "y": 3.0,
        "tag_id": "100",
        "node_id": 10,
        "offset_angle": 0.0,
        "tag_offset_angle": 0.0,
        "dir": 90.0,
        "category": 6
      }
    ],
    "paths": [
      {
        "connection": [10, 11],
        "start_pos": {"x": 1.5, "y": 1.5},
        "end_pos": {"x": 1.5, "y": 3.0}
      }
    ]
  }
}
```

<H3> Response </H3>
Code:           11003

Description:    Download map response

JSON data:      *N/A*

---

## Upload map
<H3> Request </H3>

Code:           1004 

Description:    Upload map request. \
If no layout_name is specified, the current in use layout will be uploaded

JSON data:      *table below*

| Key         | Data type | Description                           | Required | Default value |
|-------------|-----------|---------------------------------------|----------|---------------|
| layout_name | str       | The name of the layout to be uploaded | No       | -             |

<H3> Response </H3>
Code:           11004

Description:    Upload map response

JSON data:      *N/A*

| Key    | Data type         | Description                               |
|:-------|-------------------|-------------------------------------------|
| layout | [Layout](#layout) | The layout data to be uploaded from robot |

---

## Change map
<H3> Request </H3>

Code:           1005 

Description:    Change map request

JSON data:      *table below*

| Key      | Data type | Description     | Required | Default value |
|----------|-----------|-----------------|----------|---------------|
| map_name | str       | The layout name | Yes      | -             |

<H3> Response </H3>
Code:           11005

Description:    Change map response

JSON data:      *N/A*

---

## Delete map
<H3> Request </H3>

Code:           1006 

Description:    Delete map request

JSON data:      *table below*

| Key      | Data type | Description     | Required | Default value |
|----------|-----------|-----------------|----------|---------------|
| map_name | str       | The layout name | Yes      | -             |

<H3> Response </H3>
Code:           11006

Description:    Delete map response

JSON data:      *N/A*

---
