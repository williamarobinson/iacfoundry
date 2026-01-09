# IaC Foundry API Documentation

This document outlines the available API endpoints for the IaC Foundry application.

## Endpoints

### `POST /api/generate`

This is the primary endpoint for generating Terraform modules.

**Request Body:**

```json
{
  "manifest": "object",
  "githubManifestsUrl": "string",
  "resources": ["string"],
  "debug": "boolean"
}
```

-   `manifest`: (Optional) A complete manifest object. If not provided, `githubManifestsUrl` must be used.
-   `githubManifestsUrl`: (Optional) The URL to a GitHub repository directory containing manifest files. Used to fetch a manifest if one isn't provided directly.
-   `resources`: (Required) An array of resource names (e.g., `["azurerm_resource_group", "azurerm_virtual_network"]`) to generate modules for.
-   `debug`: (Optional) If `true`, the response will be JSON containing detailed debug information. Defaults to `false`.

**Response:**

-   If `debug` is `true` or the `Accept` header is `application/json`, it returns a JSON object with the generated file content and debug info.
-   Otherwise, it returns a `.zip` file containing the generated modules.

---

### `POST /api/provider-graph`

Generates a dependency graph for a given provider or a subset of its resources.

**Request Body:**

```json
{
  "manifest": "object",
  "resources": ["string"],
  "debug": "boolean",
  "getResourceListOnly": "boolean"
}
```

-   `manifest`: (Required) A valid manifest object for the provider.
-   `resources`: (Optional) A specific list of resources to analyze. If omitted, a full graph for the provider is generated.
-   `debug`: (Optional) If `true`, returns detailed debug information for each step of the analysis.
-   `getResourceListOnly`: (Optional) If `true`, the endpoint will only return a list of available resources for the provider and skip graph generation.

**Response:**

-   Returns a JSON object representing the graph with `nodes` and `edges`, along with debug info if requested.

---

### `POST /api/fetch-manifests`

Fetches and lists all available manifest files from a specified GitHub directory URL.

**Request Body:**

```json
{
  "githubManifestsUrl": "string"
}
```

-   `githubManifestsUrl`: (Required) The URL to a GitHub repository directory containing manifest files.

**Response:**

-   Returns a JSON array of all valid manifest objects found at the URL.