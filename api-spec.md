# API Specification
**5G Network Framework – Mobile Computing Project**  
**Milestone:** 3 – Interface & API Definition  
**Date:** January 2026  
**Version:** 1.0

---

## 1. Purpose

This document defines the REST API used between the **User Interface** and the **Backend Control Layer** of the 5G Network Framework.

The API enables:
- network topology visualization
- component start/stop control
- use case activation
- configuration management
- automated verification

This specification allows frontend and backend development to proceed in parallel.

---

## 2. General API Design

### 2.1 Protocol and Format
- Protocol: HTTP
- API Style: REST
- Data format: JSON
- Base path:

/api


### 2.2 Standard Response Format

All API responses follow this structure:

```json
{
  "status": "success | error",
  "message": "Description of the result",
  "data": {}
}
```
3. API Endpoints

3.1 Network Topology
GET /api/topology

Returns the current network topology and component states.

Example response:
```
{
  "status": "success",
  "data": {
    "components": [
      {
        "id": "amf",
        "type": "core",
        "status": "running",
        "ip": "172.20.0.10"
      },
      {
        "id": "gnb1",
        "type": "ran",
        "status": "running",
        "ip": "172.20.0.20"
      }
    ],
    "links": [
      {
        "from": "gnb1",
        "to": "amf",
        "protocol": "NGAP"
      }
    ]
  }
}
```

3.2 Component Control
POST /api/component/{id}/start

Starts a network component.

Example response:
```
{
  "status": "success",
  "message": "Component started"
}
```

POST /api/component/{id}/stop

Stops a network component.

3.3 Use Case Management
GET /api/usecases

Returns available predefined use cases.

Example response:
```
{
  "status": "success",
  "data": [
    {
      "id": "iot",
      "name": "Industrial IoT"
    },
    {
      "id": "v2x",
      "name": "Connected Vehicles"
    }
  ]
}
```
POST /api/usecase/activate

Activates one or more use cases.

Request body example:
```
{
  "useCases": ["iot", "v2x"]
}
```
Behavior:

Applies corresponding configuration and slicing rules

Starts required components

Triggers automated verification

3.4 Configuration Management
GET /api/configuration

Returns the active network configuration.

PUT /api/configuration

Updates network configuration parameters.

Request body example:
```
{
  "mcc": "001",
  "mnc": "01",
  "slices": [
    {
      "id": "iot-slice",
      "priority": 1,
      "bandwidth": "10Mbps"
    }
  ]
}
```
3.5 Subscriber Management (Optional)
POST /api/subscriber

Adds a subscriber profile.

Request body example:
```
{
  "imsi": "001011234567891",
  "slice": "iot-slice",
  "apn": "internet"
}
```
This endpoint abstracts database scripts such as open5gs-dbctl.

3.6 Automated Verification
POST /api/tests/run

Triggers automated verification tests.

Request body example:
```
{
  "tests": ["latency", "throughput", "connectivity"]
}
```
GET /api/tests/results

Returns the latest test results.

Example response:
```
{
  "status": "success",
  "data": [
    {
      "test": "latency",
      "result": "passed",
      "value": "12ms"
    }
  ]
}
```
4. Security Considerations

Security mechanisms such as authentication and authorization are out of scope. The API is assumed to run in a trusted environment.

5. Relation to Project Plan

Supports Milestone 3: Interface & API Definition

Enables Milestone 4: Prototype Implementation

Extendable for Milestone 5: Network slicing and transport control