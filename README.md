# DNS Record Checker & Domain Health Monitor

Full DNS lookup for any domain. Returns A, AAAA, MX, TXT, CNAME, NS, SOA records plus a smart summary that detects your mail provider, nameserver provider, and SPF/DMARC status.

## What you get

One API call returns everything:
- All DNS record types (A, AAAA, MX, TXT, CNAME, NS, SOA)
- Mail provider detection (Google Workspace, Microsoft 365, Zoho, etc.)
- Nameserver provider detection (Cloudflare, AWS Route 53, GoDaddy, etc.)
- SPF record presence check
- DMARC record presence check
- Total record count

## Who uses this

- Domain investors managing portfolios of hundreds of domains
- Security teams auditing infrastructure
- SEO agencies checking client domain health
- DevOps teams monitoring DNS configuration
- Compliance teams verifying email authentication (SPF/DMARC)

## API (Standby Mode)

This actor runs as an instant API. No cold start, no waiting.

### Check a domain

```
GET /check?domain=stripe.com
```

Response:
```json
{
  "domain": "stripe.com",
  "queriedAt": "2026-04-12T15:00:00Z",
  "records": {
    "A": ["104.18.3.10", "104.18.2.10"],
    "AAAA": [],
    "MX": [{"priority": 1, "exchange": "aspmx.l.google.com"}],
    "TXT": ["v=spf1 include:_spf.google.com ~all"],
    "CNAME": [],
    "NS": ["ns1.cloudflare.com", "ns2.cloudflare.com"],
    "SOA": {"nsname": "ns1.cloudflare.com", "hostmaster": "dns.cloudflare.com"}
  },
  "summary": {
    "hasMailServer": true,
    "mailProvider": "Google Workspace",
    "nameserverProvider": "Cloudflare",
    "hasSPF": true,
    "hasDMARC": true,
    "recordCount": 12
  }
}
```

### Health check

```
GET /health
```

## Pricing

$0.002 per domain lookup. No subscriptions, no minimum.

100 lookups = $0.20. Compare that to commercial DNS lookup APIs that charge $50+/month.

## Related actors

- [Domain WHOIS Lookup](https://apify.com/george.the.developer/domain-whois-lookup) for registration data, expiry dates, registrar info
- [Website Tech Detector](https://apify.com/george.the.developer/website-intelligence-api) for technology stack detection
- [Email Validator](https://apify.com/george.the.developer/email-validator-api) for verifying email addresses

## Built by George Kioko

48 actors on Apify, 869+ users. More at https://apify.com/george.the.developer
