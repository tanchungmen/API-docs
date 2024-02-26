<H1> TCP/IP API Docs </H1>

---
## Introduction
The robot's controller provides an interface for external system such as RCS to communicate. 
The communication is based on TCP/IP protocol suite, request/response type socket programming. 
A series of reqeust packets will be sent via the socket and the controller will revert response packets.
The packets are constructed by the header followed by the JSON data area.

Sample format of the request packets that encapsulated the header and JSON data:
![Screenshot](images/request%20packets.PNG)

Sample format of the response packets:
![Screenshot](images/response%20packets.PNG)

## API header

| Name             | Constant Value | Length (bytes) | Description                                         |
|------------------|----------------|----------------|-----------------------------------------------------|
| Head             | 0xCA00         | 2 (uint16)     | Constant value to verify the head of packets        |
| Version          | 0x0001         | 2 (uint16)     | The current version of API                          |
| Reserved         | 0x0000         | 2 (uint16)     | Reserved                                            |
| Request ID       | -              | 2 (uint16)     | The packets sent request ID                         |
| API code ID      | -              | 2 (uint16)     | The code of the request or response API             |
| JSON data length | -              | 4 (uint32)     | The length of JSON data                             |
| Reserved         | 0x0000         | 2 (uint16)     | Reserved (length is 1 byte for response)            |
| Return code      | -              | 1 (uint8)      | Return code (only in response, 0: normal, 1: error) |
| JSON data        | -              | -              | JSON data required by the API                       |


## API category
There are 3 types of API, and the API code ID and the JSON data description can be found in the following links:

| Category                      | Port Number |
|-------------------------------|-------------|
| [Config API](config.md)       | 8000        |
| [Control API](control_api.md) | 8000        |
| [Status API](status_api.md)   | 8100        |
