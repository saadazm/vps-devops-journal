# DNS and Domain Setup

## Common Records

| Type | Name | Value | Purpose |
| --- | --- | --- | --- |
| A | `@` | VPS IPv4 | Root domain |
| A | `app` | VPS IPv4 | App subdomain |
| CNAME | `www` | `example.com` | Website alias |

## Verification

```bash
dig A example.com
dig A app.example.com
```

