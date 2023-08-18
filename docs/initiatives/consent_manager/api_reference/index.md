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
    "id": "050351f2-8152-4738-9a6b-b59d1e9d0b01",
    "caId": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
    "consent_artifact": {
        "id": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
        "log": {
            "consent_use": {
                "url": "https://sample-log/api/v1/log"
            },
            "data_access": {
                "url": "https://sample-log/api/v1/log"
            }
        },
        "data": [
            "intDay",
            "intGender",
            "intMaritalStatus",
            "intMonth",
            "intPrimaryMobileNumber"
        ],
        "user": {
            "id": "safal@gmail.com"
        },
        "created": "YYYY-MM-DDThh:mm:ssZn.n",
        "expires": "2024-12-12T00:00:00.000Z",
        "purpose": "",
        "revoker": {
            "id": "did:user:123",
            "url": "https://sample-revoker/api/v1/revoke"
        },
        "consumer": {
            "id": "did:consumer:123",
            "url": "https://sample-consumer/api/v1/consume"
        },
        "provider": {
            "id": "did:proider:123",
            "url": "https://sample-consumer/api/v1"
        },
        "collector": {
            "id": "did:collector:123",
            "url": "http://64.227.181.5:6000"
        },
        "frequency": {
            "ttl": 100,
            "limit": 200
        },
        "revocable": false,
        "signature": "",
        "user_sign": "",
        "collector_sign": "",
        "total_queries_allowed": 500
    },
    "userId": "safal@gmail.com",
    "state": "CREATED",
    "created_at": "2023-08-18T05:54:59.178Z",
    "created_by": "API",
    "updated_at": "2023-08-18T05:54:59.178Z",
    "updated_by": null,
    "webhook_url": "https://sample-consumer/api/v1/consume",
    "total_attempts": 0
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
{
    "id": "050351f2-8152-4738-9a6b-b59d1e9d0b01",
    "caId": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
    "consent_artifact": {
        "id": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
        "log": {
            "consent_use": {
                "url": "https://sample-log/api/v1/log"
            },
            "data_access": {
                "url": "https://sample-log/api/v1/log"
            }
        },
        "data": [
            "intDay",
            "intGender",
            "intMaritalStatus",
            "intMonth",
            "intPrimaryMobileNumber"
        ],
        "user": {
            "id": "safal@gmail.com"
        },
        "proof": {
            "jws": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ImIxODY4YTMzLWE0OWQtNGJkMS1iYWZjLWVmYTllZDlmODgxYiIsImxvZyI6eyJjb25zZW50X3VzZSI6eyJ1cmwiOiJodHRwczovL3NhbXBsZS1sb2cvYXBpL3YxL2xvZyJ9LCJkYXRhX2FjY2VzcyI6eyJ1cmwiOiJodHRwczovL3NhbXBsZS1sb2cvYXBpL3YxL2xvZyJ9fSwiZGF0YSI6WyJpbnREYXkiLCJpbnRHZW5kZXIiLCJpbnRNYXJpdGFsU3RhdHVzIiwiaW50TW9udGgiLCJpbnRQcmltYXJ5TW9iaWxlTnVtYmVyIl0sInVzZXIiOnsiaWQiOiJzYWZhbEBnbWFpbC5jb20ifSwiY3JlYXRlZCI6IllZWVktTU0tRERUaGg6bW06c3Nabi5uIiwiZXhwaXJlcyI6IjIwMjQtMTItMTJUMDA6MDA6MDAuMDAwWiIsInB1cnBvc2UiOiIiLCJyZXZva2VyIjp7ImlkIjoiZGlkOnVzZXI6MTIzIiwidXJsIjoiaHR0cHM6Ly9zYW1wbGUtcmV2b2tlci9hcGkvdjEvcmV2b2tlIn0sImNvbnN1bWVyIjp7ImlkIjoiZGlkOmNvbnN1bWVyOjEyMyIsInVybCI6Imh0dHBzOi8vc2FtcGxlLWNvbnN1bWVyL2FwaS92MS9jb25zdW1lIn0sInByb3ZpZGVyIjp7ImlkIjoiZGlkOnByb2lkZXI6MTIzIiwidXJsIjoiaHR0cHM6Ly9zYW1wbGUtY29uc3VtZXIvYXBpL3YxIn0sImNvbGxlY3RvciI6eyJpZCI6ImRpZDpjb2xsZWN0b3I6MTIzIiwidXJsIjoiaHR0cDovLzY0LjIyNy4xODEuNTo2MDAwIn0sImZyZXF1ZW5jeSI6eyJ0dGwiOjEwMCwibGltaXQiOjIwMH0sInJldm9jYWJsZSI6ZmFsc2UsInNpZ25hdHVyZSI6IiIsInVzZXJfc2lnbiI6IiIsImNvbGxlY3Rvcl9zaWduIjoiIiwidG90YWxfcXVlcmllc19hbGxvd2VkIjo1MDAsImlhdCI6MTY5MjMzODE3NywiZXhwIjoxNjkyNzcwMTc3LCJhdWQiOiJkaWQ6Y29uc3VtZXI6MTIzIiwiaXNzIjoiY29uc2VudC1tYW5hZ2VyIiwic3ViIjoic2FmYWxAZ21haWwuY29tIn0.cBp5YAWP9aYJXZYWc0B-S6wwksELb9SWQ1yZwl37pTfBXce_9Dx9msnhXWRB9590EbzRfLT36mw41WCUXs2CzAceJqnX9Nyrd2AbMJT5bK5m6vmCkeQpAjocFw15RmiBceYSP2Zlyv9ySL0XgDwLA066ytnHZWDblCWG1wrBYfa8uOweussPWdT44Ydp48TBPq1qYs3t7EmBNl8hU_HNKKUy3dopkdYtFP9_E6buGwp2udPVwtsTuCGX8kas0QAEZZ6y4fVyuXK2RHsAURneH9NVfqIXoaqY4g_kZJmRXMlYSkby9oyNzpBmxJIZVc_XzgS-dYtzjwLunfgStnRxeQ",
            "type": "RS256",
            "created": "8/18/2023, 5:56:17 AM",
            "proofPurpose": "jwtVerify",
            "verificationMethod": "https://auth.konnect.samagra.io/.well-known/jwks"
        },
        "created": "YYYY-MM-DDThh:mm:ssZn.n",
        "expires": "2024-12-12T00:00:00.000Z",
        "purpose": "",
        "revoker": {
            "id": "did:user:123",
            "url": "https://sample-revoker/api/v1/revoke"
        },
        "consumer": {
            "id": "did:consumer:123",
            "url": "https://sample-consumer/api/v1/consume"
        },
        "provider": {
            "id": "did:proider:123",
            "url": "https://sample-consumer/api/v1"
        },
        "collector": {
            "id": "did:collector:123",
            "url": "http://64.227.181.5:6000"
        },
        "frequency": {
            "ttl": 100,
            "limit": 200
        },
        "revocable": false,
        "signature": "",
        "user_sign": "",
        "collector_sign": "",
        "total_queries_allowed": 500
    },
    "userId": "safal@gmail.com",
    "state": "ACCEPT",
    "created_at": "2023-08-18T05:54:59.178Z",
    "created_by": "API",
    "updated_at": "2023-08-18T05:54:59.178Z",
    "updated_by": null,
    "webhook_url": "https://sample-consumer/api/v1/consume",
    "total_attempts": 0
}
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
{
    "id": "050351f2-8152-4738-9a6b-b59d1e9d0b01",
    "caId": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
    "consent_artifact": {
        "id": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
        "log": {
            "consent_use": {
                "url": "https://sample-log/api/v1/log"
            },
            "data_access": {
                "url": "https://sample-log/api/v1/log"
            }
        },
        "data": [
            "intDay",
            "intGender",
            "intMaritalStatus",
            "intMonth",
            "intPrimaryMobileNumber"
        ],
        "user": {
            "id": "safal@gmail.com"
        },
        "proof": {
            "jws": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ImIxODY4YTMzLWE0OWQtNGJkMS1iYWZjLWVmYTllZDlmODgxYiIsImxvZyI6eyJjb25zZW50X3VzZSI6eyJ1cmwiOiJodHRwczovL3NhbXBsZS1sb2cvYXBpL3YxL2xvZyJ9LCJkYXRhX2FjY2VzcyI6eyJ1cmwiOiJodHRwczovL3NhbXBsZS1sb2cvYXBpL3YxL2xvZyJ9fSwiZGF0YSI6WyJpbnREYXkiLCJpbnRHZW5kZXIiLCJpbnRNYXJpdGFsU3RhdHVzIiwiaW50TW9udGgiLCJpbnRQcmltYXJ5TW9iaWxlTnVtYmVyIl0sInVzZXIiOnsiaWQiOiJzYWZhbEBnbWFpbC5jb20ifSwiY3JlYXRlZCI6IllZWVktTU0tRERUaGg6bW06c3Nabi5uIiwiZXhwaXJlcyI6IjIwMjQtMTItMTJUMDA6MDA6MDAuMDAwWiIsInB1cnBvc2UiOiIiLCJyZXZva2VyIjp7ImlkIjoiZGlkOnVzZXI6MTIzIiwidXJsIjoiaHR0cHM6Ly9zYW1wbGUtcmV2b2tlci9hcGkvdjEvcmV2b2tlIn0sImNvbnN1bWVyIjp7ImlkIjoiZGlkOmNvbnN1bWVyOjEyMyIsInVybCI6Imh0dHBzOi8vc2FtcGxlLWNvbnN1bWVyL2FwaS92MS9jb25zdW1lIn0sInByb3ZpZGVyIjp7ImlkIjoiZGlkOnByb2lkZXI6MTIzIiwidXJsIjoiaHR0cHM6Ly9zYW1wbGUtY29uc3VtZXIvYXBpL3YxIn0sImNvbGxlY3RvciI6eyJpZCI6ImRpZDpjb2xsZWN0b3I6MTIzIiwidXJsIjoiaHR0cDovLzY0LjIyNy4xODEuNTo2MDAwIn0sImZyZXF1ZW5jeSI6eyJ0dGwiOjEwMCwibGltaXQiOjIwMH0sInJldm9jYWJsZSI6ZmFsc2UsInNpZ25hdHVyZSI6IiIsInVzZXJfc2lnbiI6IiIsImNvbGxlY3Rvcl9zaWduIjoiIiwidG90YWxfcXVlcmllc19hbGxvd2VkIjo1MDAsImlhdCI6MTY5MjMzODE3NywiZXhwIjoxNjkyNzcwMTc3LCJhdWQiOiJkaWQ6Y29uc3VtZXI6MTIzIiwiaXNzIjoiY29uc2VudC1tYW5hZ2VyIiwic3ViIjoic2FmYWxAZ21haWwuY29tIn0.cBp5YAWP9aYJXZYWc0B-S6wwksELb9SWQ1yZwl37pTfBXce_9Dx9msnhXWRB9590EbzRfLT36mw41WCUXs2CzAceJqnX9Nyrd2AbMJT5bK5m6vmCkeQpAjocFw15RmiBceYSP2Zlyv9ySL0XgDwLA066ytnHZWDblCWG1wrBYfa8uOweussPWdT44Ydp48TBPq1qYs3t7EmBNl8hU_HNKKUy3dopkdYtFP9_E6buGwp2udPVwtsTuCGX8kas0QAEZZ6y4fVyuXK2RHsAURneH9NVfqIXoaqY4g_kZJmRXMlYSkby9oyNzpBmxJIZVc_XzgS-dYtzjwLunfgStnRxeQ",
            "type": "RS256",
            "created": "8/18/2023, 5:56:17 AM",
            "proofPurpose": "jwtVerify",
            "verificationMethod": "https://auth.konnect.samagra.io/.well-known/jwks"
        },
        "created": "YYYY-MM-DDThh:mm:ssZn.n",
        "expires": "2024-12-12T00:00:00.000Z",
        "purpose": "",
        "revoker": {
            "id": "did:user:123",
            "url": "https://sample-revoker/api/v1/revoke"
        },
        "consumer": {
            "id": "did:consumer:123",
            "url": "https://sample-consumer/api/v1/consume"
        },
        "provider": {
            "id": "did:proider:123",
            "url": "https://sample-consumer/api/v1"
        },
        "collector": {
            "id": "did:collector:123",
            "url": "http://64.227.181.5:6000"
        },
        "frequency": {
            "ttl": 100,
            "limit": 200
        },
        "revocable": false,
        "signature": "",
        "user_sign": "",
        "collector_sign": "",
        "total_queries_allowed": 500
    },
    "userId": "safal@gmail.com",
    "state": "DECLINE",
    "created_at": "2023-08-18T05:54:59.178Z",
    "created_by": "API",
    "updated_at": "2023-08-18T05:54:59.178Z",
    "updated_by": null,
    "webhook_url": "https://sample-consumer/api/v1/consume",
    "total_attempts": 0
}
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
{
    "id": "050351f2-8152-4738-9a6b-b59d1e9d0b01",
    "caId": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
    "consent_artifact": {
        "id": "b1868a33-a49d-4bd1-bafc-efa9ed9f881b",
        "log": {
            "consent_use": {
                "url": "https://sample-log/api/v1/log"
            },
            "data_access": {
                "url": "https://sample-log/api/v1/log"
            }
        },
        "data": [
            "intDay",
            "intGender",
            "intMaritalStatus",
            "intMonth",
            "intPrimaryMobileNumber"
        ],
        "user": {
            "id": "safal@gmail.com"
        },
        "proof": {
            "jws": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ImIxODY4YTMzLWE0OWQtNGJkMS1iYWZjLWVmYTllZDlmODgxYiIsImxvZyI6eyJjb25zZW50X3VzZSI6eyJ1cmwiOiJodHRwczovL3NhbXBsZS1sb2cvYXBpL3YxL2xvZyJ9LCJkYXRhX2FjY2VzcyI6eyJ1cmwiOiJodHRwczovL3NhbXBsZS1sb2cvYXBpL3YxL2xvZyJ9fSwiZGF0YSI6WyJpbnREYXkiLCJpbnRHZW5kZXIiLCJpbnRNYXJpdGFsU3RhdHVzIiwiaW50TW9udGgiLCJpbnRQcmltYXJ5TW9iaWxlTnVtYmVyIl0sInVzZXIiOnsiaWQiOiJzYWZhbEBnbWFpbC5jb20ifSwiY3JlYXRlZCI6IllZWVktTU0tRERUaGg6bW06c3Nabi5uIiwiZXhwaXJlcyI6IjIwMjQtMTItMTJUMDA6MDA6MDAuMDAwWiIsInB1cnBvc2UiOiIiLCJyZXZva2VyIjp7ImlkIjoiZGlkOnVzZXI6MTIzIiwidXJsIjoiaHR0cHM6Ly9zYW1wbGUtcmV2b2tlci9hcGkvdjEvcmV2b2tlIn0sImNvbnN1bWVyIjp7ImlkIjoiZGlkOmNvbnN1bWVyOjEyMyIsInVybCI6Imh0dHBzOi8vc2FtcGxlLWNvbnN1bWVyL2FwaS92MS9jb25zdW1lIn0sInByb3ZpZGVyIjp7ImlkIjoiZGlkOnByb2lkZXI6MTIzIiwidXJsIjoiaHR0cHM6Ly9zYW1wbGUtY29uc3VtZXIvYXBpL3YxIn0sImNvbGxlY3RvciI6eyJpZCI6ImRpZDpjb2xsZWN0b3I6MTIzIiwidXJsIjoiaHR0cDovLzY0LjIyNy4xODEuNTo2MDAwIn0sImZyZXF1ZW5jeSI6eyJ0dGwiOjEwMCwibGltaXQiOjIwMH0sInJldm9jYWJsZSI6ZmFsc2UsInNpZ25hdHVyZSI6IiIsInVzZXJfc2lnbiI6IiIsImNvbGxlY3Rvcl9zaWduIjoiIiwidG90YWxfcXVlcmllc19hbGxvd2VkIjo1MDAsImlhdCI6MTY5MjMzODE3NywiZXhwIjoxNjkyNzcwMTc3LCJhdWQiOiJkaWQ6Y29uc3VtZXI6MTIzIiwiaXNzIjoiY29uc2VudC1tYW5hZ2VyIiwic3ViIjoic2FmYWxAZ21haWwuY29tIn0.cBp5YAWP9aYJXZYWc0B-S6wwksELb9SWQ1yZwl37pTfBXce_9Dx9msnhXWRB9590EbzRfLT36mw41WCUXs2CzAceJqnX9Nyrd2AbMJT5bK5m6vmCkeQpAjocFw15RmiBceYSP2Zlyv9ySL0XgDwLA066ytnHZWDblCWG1wrBYfa8uOweussPWdT44Ydp48TBPq1qYs3t7EmBNl8hU_HNKKUy3dopkdYtFP9_E6buGwp2udPVwtsTuCGX8kas0QAEZZ6y4fVyuXK2RHsAURneH9NVfqIXoaqY4g_kZJmRXMlYSkby9oyNzpBmxJIZVc_XzgS-dYtzjwLunfgStnRxeQ",
            "type": "RS256",
            "created": "8/18/2023, 5:56:17 AM",
            "proofPurpose": "jwtVerify",
            "verificationMethod": "https://auth.konnect.samagra.io/.well-known/jwks"
        },
        "created": "YYYY-MM-DDThh:mm:ssZn.n",
        "expires": "2024-12-12T00:00:00.000Z",
        "purpose": "",
        "revoker": {
            "id": "did:user:123",
            "url": "https://sample-revoker/api/v1/revoke"
        },
        "consumer": {
            "id": "did:consumer:123",
            "url": "https://sample-consumer/api/v1/consume"
        },
        "provider": {
            "id": "did:proider:123",
            "url": "https://sample-consumer/api/v1"
        },
        "collector": {
            "id": "did:collector:123",
            "url": "http://64.227.181.5:6000"
        },
        "frequency": {
            "ttl": 100,
            "limit": 200
        },
        "revocable": false,
        "signature": "",
        "user_sign": "",
        "collector_sign": "",
        "total_queries_allowed": 500
    },
    "userId": "safal@gmail.com",
    "state": "REVOKED",
    "created_at": "2023-08-18T05:54:59.178Z",
    "created_by": "API",
    "updated_at": "2023-08-18T05:54:59.178Z",
    "updated_by": null,
    "webhook_url": "https://sample-consumer/api/v1/consume",
    "total_attempts": 0
}
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