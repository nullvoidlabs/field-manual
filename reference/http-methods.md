# reference/http-methods.md

## Request methods (common)
| Method | Description |
| --- | --- |
| `GET` | Requests a specific resource. Additional data can be passed via query strings in the URL (e.g. `?param=value`). |
| `POST` | Sends data to the server in the request body. Common for forms/logins and uploading data (e.g., images/documents). |
| `HEAD` | Requests headers only (as if `GET`), without the response body. Often used to check response length/metadata. |
| `PUT` | Creates new resources on the server. If enabled without proper controls, can allow uploading malicious resources. |
| `DELETE` | Deletes an existing resource. If not properly secured, can lead to DoS by deleting critical files. |
| `OPTIONS` | Returns information about the server, such as accepted methods. |
| `PATCH` | Applies partial modifications to a resource at the specified location. |

⚠️ External reference for a full list of methods:
    https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods
