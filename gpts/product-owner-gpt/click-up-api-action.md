# ClickUp API Action

## Authentication
Authentication Type: API Key
API Key: Paste your ClickUp API token. Generate it from your ClickUp account settings.
Auth Type: Custom
Custom Header Name: Authorization

## OpenAPI Schema

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "ClickUp Create Task API",
    "version": "1.0.0",
    "description": "API for creating tasks in a ClickUp list"
  },
  "servers": [
    {
      "url": "https://api.clickup.com/api/v2",
      "description": "ClickUp API Server"
    }
  ],
  "paths": {
    "/list/{list_id}/task": {
      "post": {
        "operationId": "createTask",
        "security": [
          {
            "ClickUpAuth": []
          }
        ],
        "summary": "Create a new task in the specified ClickUp list",
        "parameters": [
          {
            "name": "list_id",
            "in": "path",
            "description": "ID of the ClickUp list where the task will be created",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "description": "Task creation payload",
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "name": {
                    "type": "string",
                    "description": "The name/title of the task"
                  },
                  "markdown_content": {
                    "type": "string",
                    "description": "The task description in Markdown format"
                  },
                  "custom_item_id": {
                    "type": "integer",
                    "description": "A custom identifier for the task"
                  }
                },
                "required": [
                  "name",
                  "markdown_content"
                ]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Task created successfully",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Task"
                }
              }
            }
          },
          "400": {
            "description": "Invalid request payload"
          },
          "401": {
            "description": "Unauthorized (invalid or missing API token)"
          }
        }
      }
    }
  },
  "components": {
    "securitySchemes": {
      "ClickUpAuth": {
        "type": "apiKey",
        "in": "header",
        "name": "Authorization",
        "description": "Add your ClickUp API token here, e.g. `Authorization: pk_xxxxxxxx`"
      }
    },
    "schemas": {
      "Task": {
        "type": "object",
        "properties": {
          "id": {
            "type": "string",
            "description": "Unique identifier of the created task"
          },
          "name": {
            "type": "string",
            "description": "Name of the task"
          },
          "markdown_content": {
            "type": "string",
            "description": "Task description in Markdown"
          },
          "custom_item_id": {
            "type": "integer",
            "description": "Custom identifier provided for the task"
          },
          "status": {
            "type": "string",
            "description": "Current status of the task"
          }
        },
        "required": [
          "id",
          "name"
        ]
      }
    }
  }
}
```
