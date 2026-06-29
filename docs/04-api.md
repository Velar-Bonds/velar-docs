# API REST

Base URL: `http://localhost:3001/api` (prefijo global `api`).

Documentación interactiva: `GET /api/docs` (Swagger / OpenAPI).

Recursos principales: `auth`, `bonds`, `transfers`, `parties`, `audit`, `analytics`,
`notifications`, `health`. Endpoints de escritura validan la entrada con DTOs
(`class-validator`). El endpoint canónico de trazabilidad es
`GET /api/audit/bonds/:tokenId/traceability`.
