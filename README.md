# scrapy.net

scrapy.net is a simple web scraper api, built on .NET, docker and Selenium.

## Schema

```json
{
  "openapi": "3.0.1",
  "info": {
    "title": "scrapy",
    "version": "v1"
  },
  "paths": {
    "/requestUri": {
      "post": {
        "tags": [
          "Scrapy"
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/UriRequest"
              }
            },
            "text/json": {
              "schema": {
                "$ref": "#/components/schemas/UriRequest"
              }
            },
            "application/*+json": {
              "schema": {
                "$ref": "#/components/schemas/UriRequest"
              }
            }
          }
        },
        "responses": {
          "202": {
            "description": "Success"
          },
          "400": {
            "description": "Bad Request",
            "content": {
              "text/plain": {
                "schema": {
                  "$ref": "#/components/schemas/ProblemDetails"
                }
              },
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ProblemDetails"
                }
              },
              "text/json": {
                "schema": {
                  "$ref": "#/components/schemas/ProblemDetails"
                }
              }
            }
          }
        }
      }
    },
    "/requestId": {
      "get": {
        "tags": [
          "Scrapy"
        ],
        "parameters": [
          {
            "name": "requestId",
            "in": "query",
            "schema": {
              "type": "string",
              "format": "uuid"
            }
          },
          {
            "name": "resourceType",
            "in": "query",
            "schema": {
              "$ref": "#/components/schemas/ResourceType"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Success"
          },
          "404": {
            "description": "Not Found",
            "content": {
              "text/plain": {
                "schema": {
                  "$ref": "#/components/schemas/ProblemDetails"
                }
              },
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/ProblemDetails"
                }
              },
              "text/json": {
                "schema": {
                  "$ref": "#/components/schemas/ProblemDetails"
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "ProblemDetails": {
        "type": "object",
        "properties": {
          "type": {
            "type": "string",
            "nullable": true
          },
          "title": {
            "type": "string",
            "nullable": true
          },
          "status": {
            "type": "integer",
            "format": "int32",
            "nullable": true
          },
          "detail": {
            "type": "string",
            "nullable": true
          },
          "instance": {
            "type": "string",
            "nullable": true
          }
        },
        "additionalProperties": { }
      },
      "ResourceType": {
        "enum": [
          "PageSource",
          "Screenshot"
        ],
        "type": "string"
      },
      "UriRequest": {
        "type": "object",
        "properties": {
          "uriString": {
            "type": "string",
            "nullable": true
          },
          "resourceType": {
            "$ref": "#/components/schemas/ResourceType"
          }
        },
        "additionalProperties": false
      }
    }
  }
}
```