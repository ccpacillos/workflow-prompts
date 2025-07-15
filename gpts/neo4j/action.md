# GPT Action Config
This config file defines the action that the custom GPT will use to interact with the Neo4j database through HTTP connection.

## Authentication
- Authentication Type: `API Key`
- API Key: `<base64-encoded "username:password">`
- Auth Type: `Basic`

## Schema
Note: Replace `url` with the actual endpoint URL of your Neo4j database.

```yaml
openapi: 3.1.0
info:
  title: Neo4j Cypher Runner
  version: 1.0.0
servers:
  - url: https://your.neo4j.url/db/neo4j/tx/commit
paths:
  /:
    post:
      summary: Execute a batch of Cypher statements
      operationId: runCypherBatch
      security:
        - BasicAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                statements:
                  type: array
                  items:
                    type: object
                    properties:
                      statement:
                        type: string
                      parameters:
                        type: object
                        additionalProperties: true
                    required:
                      - statement
              required:
                - statements
      responses:
        '200':
          description: Successful Cypher execution
          content:
            application/json:
              schema:
                type: object
                properties:
                  results:
                    type: array
                    items:
                      type: object
                  errors:
                    type: array
                    items:
                      type: object
        '400':
          description: Invalid input
        '500':
          description: Internal server error
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic
  schemas: {}

```
