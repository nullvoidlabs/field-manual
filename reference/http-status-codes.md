# reference/http-status-codes.md

## Status code classes
| Code class | Meaning |
| --- | --- |
| `1xx` | Provides information and does not affect the processing of the request. |
| `2xx` | Returned when a request succeeds. |
| `3xx` | Returned when the server redirects the client. |
| `4xx` | Signifies improper requests `from the client` (e.g., resource doesn't exist, bad format). |
| `5xx` | Returned when there is some problem `with the HTTP server` itself. |

## Common HTTP response codes
| Code | Description |
| --- | --- |
| `200 OK` | Returned on a successful request, and the response body usually contains the requested resource. |
| `302 Found` | Redirects the client to another URL (e.g., redirecting to a dashboard after login). |
| `400 Bad Request` | Returned on encountering malformed requests (e.g., missing line terminators). |
| `403 Forbidden` | Client doesn't have appropriate access to the resource; can also be returned when the server detects malicious input. |
| `404 Not Found` | Resource doesn't exist on the server. |
| `500 Internal Server Error` | Server cannot process the request. |

## References (non-exhaustive)
- `https://developer.mozilla.org/en-US/docs/Web/HTTP/Status`
- `https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes`
- `https://docs.aws.amazon.com/AmazonSimpleDB/latest/DeveloperGuide/APIError.html`
