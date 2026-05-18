# Network Appliance REST API Guide — Portfolio Sample

## Overview

The Network Appliance REST API allows administrators and integration teams to configure, monitor, and manage a virtual network appliance through standard HTTP methods.

This sample demonstrates how REST API documentation can be structured for a network infrastructure product. It includes request structure, authentication, headers, response format, status codes, and sample API workflows.

> **Note:** This is a sanitized portfolio sample. Product names, company names, IP addresses, endpoints, version numbers, and proprietary values have been replaced with generic examples.

---

## Audience

This guide is intended for:

- Network administrators
- System administrators
- DevOps engineers
- Integration engineers
- QA engineers
- Technical support teams

---

## Use Cases

You can use the REST API to perform the following tasks:

- Query system and appliance configuration
- Update system settings
- Configure network services
- Create or update resource objects
- Delete resource objects
- Integrate appliance management into automation workflows

---

## REST API Request and Response Flow

The REST API follows a standard request and response model.

1. The client sends an HTTP or HTTPS request to the appliance.
2. The appliance validates the request and authenticates the user.
3. The appliance processes the requested operation.
4. The appliance returns a response with a status code and response body.

---

## Base URL Format

Use the following format to send API requests:

```text
https://<management-ip>:<port>/api/v1/<resource-path>
```

### Example

```text
https://192.0.2.10:9443/api/v1/system/host-settings
```

### URL Components

| Component | Description |
|---|---|
| `https` | Protocol used to connect to the appliance. |
| `<management-ip>` | Management IP address of the appliance. |
| `<port>` | REST API service port. |
| `/api/v1` | API version path. |
| `<resource-path>` | Path that identifies the resource to query or configure. |

---

## Supported HTTP Methods

| Method | Description | Example Use Case |
|---|---|---|
| `GET` | Retrieves information about a resource. | Query system status or configuration. |
| `POST` | Creates a resource or performs an action. | Create a remote log server entry or start an appliance instance. |
| `PUT` | Updates an existing resource or setting. | Update hostname or service configuration. |
| `DELETE` | Deletes a resource. | Delete an administrator account or configuration object. |

---

## Authentication

The REST API uses Basic Authentication.

Each request must include a valid `Authorization` header. The username and password must belong to an administrator account that has permission to perform the requested operation.

### Header Format

```text
Authorization: Basic <base64-encoded-credentials>
```

### Example

```text
Authorization: Basic <encoded-value>
```

> **Security Note:** Do not expose usernames, passwords, or encoded credentials in scripts, logs, screenshots, or public repositories.

---

## Request Headers

| Header | Required | Description |
|---|---|---|
| `Authorization` | Yes | Authenticates the API request. |
| `Accept` | Yes | Defines the expected response format. |
| `Content-Type` | Required for `POST` and `PUT` | Defines the request body format. |

---

## Supported Response Formats

The API can return response data in JSON or XML format.

| Format | Header Value |
|---|---|
| JSON | `application/json` |
| XML | `application/xml` |

### JSON Header Example

```text
Accept: application/json
Content-Type: application/json
```

---

## Common Status Codes

| Status Code | Description |
|---|---|
| `200 OK` | The request was successful. |
| `201 Created` | The resource was created successfully. |
| `202 Accepted` | The request was accepted for processing. |
| `204 No Content` | The resource was deleted successfully. |
| `400 Bad Request` | The request is invalid or required fields are missing. |
| `401 Unauthorized` | Authentication failed. |
| `403 Forbidden` | The user does not have permission to perform the operation. |
| `404 Not Found` | The requested resource was not found. |
| `405 Method Not Allowed` | The HTTP method is not supported for the resource. |
| `500 Internal Server Error` | The server encountered an unexpected error. |
| `503 Service Unavailable` | The REST API service is unavailable. |

---

# Before Using the REST API

Before sending API requests, complete the following setup tasks.

## Prerequisites

Ensure that:

- The appliance is powered on and reachable through the management network.
- The REST API service is enabled.
- The API service port is open in the firewall.
- An administrator account is available.
- The API client supports custom headers and JSON request bodies.
- HTTPS certificate warnings are reviewed and handled according to your organization’s security policy.

---

## Enable the REST API Service

Use the appliance CLI or administrator console to enable the REST API service.

### Example CLI Command

```text
restapi enable https 9443
```

### Expected Result

The appliance enables the REST API service on HTTPS port `9443`.

---

## Create an API Administrator Account

Create an administrator account with the required access privilege.

### Example CLI Command

```text
user apiadmin <password> admin
```

> **Note:** Use a strong password and follow your organization’s credential management policy.

---

## Configure an API Client

You can use tools such as Postman, REST Client, or curl to test the API.

Configure the following values in the API client:

| Setting | Value |
|---|---|
| Method | `GET`, `POST`, `PUT`, or `DELETE` |
| URL | REST API endpoint URL |
| Authorization | Basic Authentication |
| Accept Header | `application/json` |
| Content-Type Header | `application/json` |

---

# API Reference Examples

The following examples show common API operations for a network appliance.

---

## Example 1: Query Host Settings

Use this API to retrieve the current hostname configured on the appliance.

### Method

```text
GET
```

### Endpoint

```text
/api/v1/system/host-settings
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
```

### Request Body

No request body is required.

### Sample Response

```json
{
  "host_settings": {
    "hostname": "network-appliance-01"
  }
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| `hostname` | String | Hostname configured on the appliance. |

---

## Example 2: Update Hostname

Use this API to update the appliance hostname.

### Method

```text
PUT
```

### Endpoint

```text
/api/v1/system/host-settings/hostname
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
Content-Type: application/json
```

### Sample Request

```json
{
  "hostname": "network-appliance-prod"
}
```

### Sample Response

```json
{
  "host_settings": {
    "hostname": "network-appliance-prod"
  }
}
```

### Result

The appliance updates the hostname and returns the updated value in the response.

---

## Example 3: Query NTP Settings

Use this API to view the NTP configuration and synchronization status.

### Method

```text
GET
```

### Endpoint

```text
/api/v1/system/ntp-settings
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
```

### Sample Response

```json
{
  "ntp_settings": {
    "enabled": true,
    "servers": [
      {
        "server": "192.0.2.20",
        "priority": 1,
        "status": "synchronized"
      },
      {
        "server": "192.0.2.21",
        "priority": 2,
        "status": "available"
      }
    ]
  }
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| `enabled` | Boolean | Indicates whether NTP is enabled. |
| `server` | String | IP address or hostname of the NTP server. |
| `priority` | Number | Priority assigned to the NTP server. |
| `status` | String | Current synchronization status. |

---

## Example 4: Update SNMP Settings

Use this API to enable or disable SNMP monitoring.

### Method

```text
PUT
```

### Endpoint

```text
/api/v1/admin/snmp/general
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
Content-Type: application/json
```

### Sample Request

```json
{
  "snmp": {
    "enabled": true,
    "version": "v3",
    "contact": "network-admin@example.com",
    "location": "Data Center 1"
  }
}
```

### Sample Response

```json
{
  "snmp": {
    "enabled": true,
    "version": "v3",
    "contact": "network-admin@example.com",
    "location": "Data Center 1"
  }
}
```

### Result

The appliance updates the SNMP configuration.

---

## Example 5: Create a Remote Syslog Server

Use this API to add a remote Syslog server for log forwarding.

### Method

```text
POST
```

### Endpoint

```text
/api/v1/admin/logging/syslog-servers
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
Content-Type: application/json
```

### Sample Request

```json
{
  "syslog_server": {
    "ip_address": "192.0.2.50",
    "port": 514,
    "protocol": "udp"
  }
}
```

### Sample Response

```json
{
  "syslog_server": {
    "id": "192.0.2.50-514-udp",
    "ip_address": "192.0.2.50",
    "port": 514,
    "protocol": "udp",
    "status": "created"
  }
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| `id` | String | Unique identifier of the Syslog server entry. |
| `ip_address` | String | IP address of the remote Syslog server. |
| `port` | Number | Syslog server port. |
| `protocol` | String | Transport protocol used for log forwarding. |
| `status` | String | Creation status of the Syslog server entry. |

---

## Example 6: Create a Virtual Appliance Instance

Use this API to create a virtual appliance instance from an available image.

### Method

```text
POST
```

### Endpoint

```text
/api/v1/virtual-appliances/instances
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
Content-Type: application/json
```

### Sample Request

```json
{
  "instance": {
    "name": "va-instance-01",
    "size": "small",
    "image": "default-image"
  }
}
```

### Sample Response

```json
{
  "instance": {
    "id": "va-instance-01",
    "name": "va-instance-01",
    "size": "small",
    "image": "default-image",
    "status": "created"
  }
}
```

### Result

The appliance creates a virtual appliance instance using the specified image.

---

## Example 7: Start a Virtual Appliance Instance

Use this API to start an existing virtual appliance instance.

### Method

```text
POST
```

### Endpoint

```text
/api/v1/virtual-appliances/instances/start
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
Content-Type: application/json
```

### Sample Request

```json
{
  "target": "va-instance-01"
}
```

### Sample Response

```json
{
  "operation": {
    "target": "va-instance-01",
    "status": "accepted",
    "message": "Start operation has been submitted."
  }
}
```

---

## Example 8: Shut Down a Virtual Appliance Instance

Use this API to shut down an existing virtual appliance instance.

### Method

```text
POST
```

### Endpoint

```text
/api/v1/virtual-appliances/instances/shutdown
```

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
Content-Type: application/json
```

### Sample Request

```json
{
  "target": "va-instance-01"
}
```

### Sample Response

```json
{
  "operation": {
    "target": "va-instance-01",
    "status": "accepted",
    "message": "Shutdown operation has been submitted."
  }
}
```

---

## Example 9: Delete an Administrator Account

Use this API to delete a specific administrator account.

### Method

```text
DELETE
```

### Endpoint

```text
/api/v1/system/administrators/{username}
```

### Path Parameter

| Parameter | Type | Required | Description |
|---|---|---|---|
| `username` | String | Yes | Username of the administrator account to delete. |

### Request Headers

```text
Authorization: Basic <encoded-value>
Accept: application/json
```

### Request Body

No request body is required.

### Sample Response

```json
{
  "message": "Administrator account deleted successfully."
}
```

---

# Error Response Format

When an API request fails, the appliance returns an error response.

## Sample Error Response

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "The required field is missing.",
    "details": "Provide a valid hostname and try again."
  }
}
```

## Error Fields

| Field | Type | Description |
|---|---|---|
| `code` | String | Application-specific error code. |
| `message` | String | Short description of the error. |
| `details` | String | Additional information to help resolve the issue. |

---

# Troubleshooting

| Issue | Possible Cause | Resolution |
|---|---|---|
| API returns `401 Unauthorized` | Invalid username, password, or encoded credential. | Verify the administrator account and authentication header. |
| API returns `403 Forbidden` | User does not have permission for the requested operation. | Assign the required role or privilege to the user. |
| API returns `404 Not Found` | Endpoint path or resource ID is incorrect. | Verify the endpoint URL and resource identifier. |
| API returns `405 Method Not Allowed` | HTTP method is not supported for the endpoint. | Use the correct method for the resource. |
| API returns `503 Service Unavailable` | REST API service is disabled or unreachable. | Verify that the REST API service is enabled and the port is open. |
| JSON response is not returned | Accept header is missing or incorrect. | Set the `Accept` header to `application/json`. |
| HTTPS warning appears | Certificate is self-signed or not trusted by the client. | Add the certificate to the trusted store based on your organization’s security policy. |

---

# Best Practices

- Use HTTPS for all API requests.
- Use least-privilege administrator accounts.
- Do not expose credentials in scripts, logs, screenshots, or public repositories.
- Use generic sample data in public documentation.
- Validate request payloads before sending API calls.
- Include clear error handling in automation scripts.
- Use consistent endpoint naming and response examples.
- Test API workflows before publishing documentation.
- Keep request and response examples aligned with the latest product behavior.

---

# Documentation Skills Demonstrated

This sample demonstrates:

- REST API documentation for network infrastructure products
- Request and response structure
- HTTP method explanation
- Authentication documentation
- Header documentation
- JSON request and response examples
- Status code documentation
- Network configuration workflow writing
- Troubleshooting guidance
- Sanitized enterprise documentation sample creation
- Developer-focused and administrator-focused documentation style
