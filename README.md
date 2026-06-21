# Evil-DB Blocklists

Free, no-signup threat-intelligence blocklists from **[Evil-DB](https://evil-db.io)** — a community threat-intelligence database aggregating ~70 public feeds into malicious IPs, malware/phishing domains, and botnet C2 infrastructure.

These files are plain text, directly subscribable, and refreshed regularly. Use them in Pi-hole, pfBlockerNG/pfSense, OPNsense, AdGuard Home, BIND/Unbound, iptables/ipset, or any tool that ingests a URL.

> No API key, no account. If a list saves you time, consider [supporting the project](https://evil-db.io/pricing).

## Lists

| List | Type | Format | Raw URL |
|------|------|--------|---------|
| Malware IPs | IPs | plain | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/ips/malware-ips.txt` |
| Spam Sources | IPs | plain | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/ips/spam-sources.txt` |
| Botnet C2 | IPs | plain | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/ips/botnet-c2.txt` |
| Ad & Tracker Domains | Domains | plain | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/domains/ads-trackers.txt` |
| Ad & Tracker Domains | Domains | hosts | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/domains/ads-trackers.hosts` |
| Phishing Domains | Domains | plain | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/domains/phishing-domains.txt` |
| Phishing Domains | Domains | hosts | `https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/domains/phishing-domains.hosts` |

The live API also serves these (and more formats — RPZ, CSV, JSON, Snort/Suricata) at
`https://evil-db.io/api/v1/blocklists/<slug>?format=<format>`.

## Usage

**Pi-hole / AdGuard Home** — add a domain list (`.hosts` or plain):
```
https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/domains/phishing-domains.hosts
```

**pfBlockerNG / pfSense / OPNsense** — add an IP list as a URL feed:
```
https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/ips/malware-ips.txt
```

**iptables + ipset:**
```bash
curl -s https://raw.githubusercontent.com/B33BMO/evildb-blocklists/main/ips/malware-ips.txt \
  | grep -E '^[0-9]' | while read ip; do ipset add evildb "$ip"; done
```

**BIND / Unbound RPZ** (domain lists, via the API):
```
https://evil-db.io/api/v1/blocklists/phishing-domains?format=rpz
```

## Notes

- Entries are aggregated from public threat feeds with confidence scoring; treat them as advisory.
- **False positive?** Report it at <https://evil-db.io> and it'll be reviewed.
- These lists are provided as-is, no warranty. Always test before blocking in production.

— Generated from [evil-db.io](https://evil-db.io)
