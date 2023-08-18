---
sidebar_position: 3
sidebar_label: API Reference
---
# Consent Manager - API Reference
This section highlights the key apis accessible along with their capabilites, request body and appropriate response.

## Authentication
All requests to the Consent Manager APIs must include an authentication token in the request headers. To authenticate, add an `Authorization` header with the value `Bearer YOUR_TOKEN` in your HTTP requests.

## Endpoints

### Register a new Consent Artifact
This allows to create a new consent artifact and associate it with a user.

**Endpoint**: `/auth/register`

**HTTP Method**: POST

**Request Headers**:
- `Content-Type: application/json`
- `Authorization: Bearer YOUR_TOKEN`

**Request Body**:

```json
{
    "consentArtifact": {
        "signature": "",
        "created": "YYYY-MM-DDThh:mm:ssZn.n",
        "expires": "2024-12-12T00:00:00.000Z",
        "id": "",
        "revocable": false,
        "collector": {
            "id": "did:collector:123",
            "url": "http://64.227.181.5:6000"
        },
        "consumer": {
            "id": "did:consumer:123",
            "url": "https://sample-consumer/api/v1/consume"
        },
        "provider": {
            "id": "did:proider:123",
            "url": "https://sample-consumer/api/v1"
        },
        "user": {
            "id": "safal@gmail.com"
        },
        "revoker": {
            "url": "https://sample-revoker/api/v1/revoke",
            "id": "did:user:123"
        },
        "purpose": "",
        "user_sign": "",
        "collector_sign": "",
        "frequency": {
            "ttl": 100,
            "limit": 200
        },
        "total_queries_allowed": 500,
        "log": {
            "consent_use": {
                "url": "https://sample-log/api/v1/log"
            },
            "data_access": {
                "url": "https://sample-log/api/v1/log"
            }
        },
        "data": ["intDay","intGender","intMaritalStatus","intMonth","intPrimaryMobileNumber"]
    }
}
```
**Example Response**:
```json
{
  "status": "success",
  "message": "User created successfully",
  "data": {
    "id": 789012,
    "username": "new_user",
    "email": "new_user@example.com",
    "created_at": "2023-08-17T12:34:56Z"
  }
}
```

### ACCEPT a Consent Artifact
Enables you to accept the created consent artifact which means you are granting permission to use the authorized information.

**Endpoint**: `/auth/:caId/accept`

**HTTP Method**: PATCH

**Request Headers**:
- `Content-Type: application/json`
- `Authorization: Bearer YOUR_TOKEN`

**Request Parameters**:
- `caId: ID of the newly created Consent Artifact`

**Example Response**:
```json
```

### REJECT a Consent Artifact
Enables you to reject the created consent artifact which means the requested information will not be allowed for access.

**Endpoint**: `/auth/:caId/reject`

**HTTP Method**: PATCH

**Request Headers**:
- `Content-Type: application/json`
- `Authorization: Bearer YOUR_TOKEN`

**Request Parameters**:
- `caId: ID of the newly created Consent Artifact`

**Example Response**:
```json
```

### REVOKE a Consent Artifact
This allows you to REVOKE previously granted permissions, meaning, in a case you have changed your mind and don't want your data to be accessed now, you can simply revoke the Consent Artifact.

**Endpoint**: `/auth/:caId/revoke`

**HTTP Method**: PATCH

**Request Headers**:
- `Content-Type: application/json`
- `Authorization: Bearer YOUR_TOKEN`

**Request Parameters**:
- `caId: ID of the newly created Consent Artifact`

**Example Response**:
```json
```

### Retrieve requested data 
Allows to retrieve the requested data from the backend. 

**Endpoint**: `/auth/verify`

**HTTP Method**: POST

**Request Headers**:
- `Content-Type: application/json`
- `Authorization: Bearer YOUR_TOKEN`

**Request Body for REST implementation**:
```json
{
    "caId": "db01b2d7-1575-4431-9ecd-dcd70aba83f3",
    "requestType": "REST",
    "queryObject": {
        "method": "POST",
        "headers": {},
        "body": {
             "aadhaar_no": "49827XXXX952"
        },
        "data": ["intDay","intGender","intMaritalStatus","intMonth","intPrimaryMobileNumber"]
    }
}
```

**Request Body for GQL implementation**:
```json
{
    "caId": "db01b2d7-1575-4431-9ecd-dcd70aba83f3",
    "requestType": "GQL",
    "gql": "query MyQuery { query_resolver_table(where: {vch_aadharno: {_eq: \"49827XXXX952\"}}) { int_day int_farmer_type int_gender int_krushk_id int_marital_status int_month vch_farmer_name vch_father_name vch_gp_ward vch_district } }"
}
```

**Example Response**:
```json
{
    "int_day": "6",
    "int_farmer_type": "4",
    "int_gender": "2",
    "int_krushk_id": "344XXX0",
    "int_marital_status": "2",
    "int_month": "3",
    "vch_farmer_name": "TEST USER",
    "vch_father_name": null,
    "vch_gp_ward": "275086",
    "vch_district": "363"
}
```