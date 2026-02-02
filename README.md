# WireMock POC – Internal Mock API Service

### Purpose

This project provides an internal mock API service for frontend, QA, and integration testing without relying on live backend APIs.

### Folder Structure

- `mappings/` – JSON files defining request/response mappings (endpoints)
- `_files/` – optional static response files (JSON, images, etc.)
- `docker-compose.yml` – WireMock container setup

### Start WireMock

```bash
docker-compose up -d
---
```

- Access WireMock at http://localhost:8080

- Example: http://localhost:8080/api/v1/customers/123

### Adding a New Endpoint

1. Copy the template JSON from mappings/template.json

2. Update:

- method: GET, POST, etc.
- urlPathPattern: /api/v1/YOUR_ENDPOINT
- jsonBody: define response payload
- status: HTTP status code

3. Save as mappings/<your-endpoint-name>.json

### Dynamic Fields (Response Templating)

- {{guid}} → random GUID
- {{now}} → current timestamp (ISO 8601)
- {{randomValue type='ALPHANUMERIC' length=5}} → random string
- {{randomValue type='number' min=1000 max=9999}} → random number

### Testing

- GET endpoints: open in browser or Postman

- POST endpoints: send JSON payload in Postman

- Example payload:

```bash
{
  "email": "user1@example.com",
  "password": "password123"
}
```

### Notes

- \_files/ folder is optional unless bodyFileName is used

- Multiple scenarios (200, 400, 401) can be defined by creating separate mapping files
