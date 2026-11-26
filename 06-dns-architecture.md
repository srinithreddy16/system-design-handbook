# DNS System Architecture

## DNS Architecture

### The players

| Component | Role |
| --- | --- |
| DNS Resolver | Provided by your ISP (or router). Does the lookup work on your behalf. |
| Root Server | Top of the hierarchy. Knows which TLD servers to ask. |
| TLD Server | Handles one top-level domain (.com, .net, ...). Knows which name server to ask. |
| Authoritative Name Server | Holds the real IP address for the domain. |

### What are root servers?

- There are 13 root server addresses, named A to M.
- They are run by various organizations, and each has many physical copies spread around the world.
- You don't need to memorize who runs them.

### What are TLDs (Top-Level Domains)?

The last part of a domain: .com, .net, .gov, .in, .uk, .us, .edu, etc.

### The lookup step by step

Looking up telescope.com:

```
Your machine
     │
     ▼
DNS Resolver (via your ISP / router)
     │
     ├─ 1) Ask ROOT SERVER ────────────> "I don't know telescope.com,
     │                                    but here is the .com TLD server"
     │
     ├─ 2) Ask TLD SERVER (.com) ──────> "Here is the authoritative name server
     │                                    for telescope.com"
     │
     └─ 3) Ask AUTHORITATIVE NAME SERVER > "telescope.com is at <IP address>"
     │
     ▼
Browser connects to that IP and gets the web page
```

In words:

1. The resolver asks a root server. It doesn't know the site, but it knows who handles .com.
2. The resolver asks the .com TLD server. It doesn't have the final IP, but it knows the authoritative name server for the domain.
3. The resolver asks the authoritative name server, which returns the actual IP address.
4. The browser uses that IP to load the site.

Authoritative name servers are usually configured through providers like GoDaddy or Hostinger, wherever you manage your domain.

### Caching: avoiding the 3-step lookup every time

Doing three lookups for every click would be slow, so the result is cached. The full lookup happens the first time. Later requests use the saved answer.

Cache locations:

- Browser cache
- OS (operating system) cache
- DNS resolver cache (holds commonly requested domains)

### Zones

When you create a domain and its subdomains, they form a zone on the authoritative name server.

- One zone holds the domain and all its subdomains.
- Example: the telescope.com zone contains telescope.com, courses.telescope.com, docs.telescope.com, and so on.
- When someone looks up courses.telescope.com, the authoritative name server finds the telescope.com zone and returns the right IP from it.

## Quick Summary

| Concept | One-line meaning |
| --- | --- |
| DNS | Translates domain names into IP addresses |
| Domain | Main site name (telescope.com) |
| Subdomain | Section under a domain (docs.telescope.com) |
| DNS Resolver | Does the lookup for you (ISP or router) |
| Root Server | Points to the right TLD server |
| TLD Server | Points to the right authoritative name server |
| Authoritative Name Server | Gives the final IP address |
| Cache | Saved results (browser, OS, resolver) to skip repeat lookups |
| Zone | A domain plus all its subdomains on the name server |

## Why DNS is well designed

- Hierarchical: the work is split across root, TLD, and authoritative levels
- Distributed: no single server holds everything, so there is no single point of failure
- Cached: repeat lookups are fast
- Flexible: a site can change its IP and only the authoritative server needs updating

Note: the source transcript ends as the next topic begins, so these notes cover everything up to that point.
