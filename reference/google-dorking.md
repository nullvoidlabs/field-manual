# reference/google-dorking.md

## Search operators (Google)
| Operator | Outcome | Example | Example outcome |
| --- | --- | --- | --- |
| `site:` | Limit results to a specific site/domain | `site:example.com` | Pages on example.com |
| `inurl:` | Term appears in URL | `inurl:login` | Login pages |
| `filetype:` | File extension/type | `filetype:pdf` | PDFs |
| `intitle:` | Term appears in page title | `intitle:"confidential report"` | Title matches phrase |
| `intext:` / `inbody:` | Term appears in page body | `intext:"password reset"` | Pages containing phrase |
| `cache:` | Cached page (if available) | `cache:example.com` | Cached view |
| `link:` | Pages linking to a URL | `link:example.com` | Backlinks |
| `related:` | Similar sites | `related:example.com` | Related domains |
| `info:` | Basic info summary | `info:example.com` | Summary info |
| `define:` | Definition lookup | `define:phishing` | Definitions |
| `numrange:` | Numbers in range | `site:example.com numrange:1000-2000` | Pages with numbers in range |
| `allintext:` | All terms in body text | `allintext:admin password reset` | Body contains all terms |
| `allinurl:` | All terms in URL | `allinurl:admin panel` | URL contains all terms |
| `allintitle:` | All terms in title | `allintitle:confidential report 2023` | Title contains all terms |
| `AND` | Require both sides | `site:example.com AND (inurl:admin OR inurl:login)` | Constrain results |
| `OR` | Either term | `"linux" OR "ubuntu" OR "debian"` | Any term matches |
| `NOT` | Exclude term | `site:bank.com NOT inurl:login` | Excluding matches |
| `*` | Wildcard | `site:socialnetwork.com filetype:pdf user* manual` | Wildcard term |
| `..` | Numeric range | `site:ecommerce.com "price" 100..500` | Values in range |
| `"..."` | Exact phrase | `"information security policy"` | Exact phrase match |
| `-` | Exclude term | `site:news.com -inurl:sports` | Excluding URLs |

## Common query patterns (examples)
### Login/admin pages
- `site:example.com inurl:login`
- `site:example.com (inurl:login OR inurl:admin)`

### Exposed files
- `site:example.com filetype:pdf`
- `site:example.com (filetype:xls OR filetype:docx)`

### Config files
- `site:example.com inurl:config.php`
- `site:example.com (ext:conf OR ext:cnf)`

### Backups / dumps
- `site:example.com inurl:backup`
- `site:example.com filetype:sql`

## Reference
- Google Hacking Database (GHDB): https://www.exploit-db.com/google-hacking-database
