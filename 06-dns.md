# Domain Name System (DNS)

How does a browser turn a name like telescope.com into a server it can actually talk to?

## Chapter 12: What is DNS and Why Do We Need It?

### The problem

- Humans use names: 
- Computers communicate using IP addresses: e.g. 192.0.2.1

So something must sit between the browser and the internet to translate a domain name into an IP address. That is DNS (Domain Name System).

```
Browser: "telescope.com"  ──>  DNS  ──>  "192.0.2.1"  ──>  Browser contacts that server
```

### Domain vs Subdomain

| Term | Example | Meaning |
| --- | --- | --- |
| Domain | telescope.com, google.com | The main website name |
| Subdomain | docs.telescope.com, courses.telescope.com | Sections created under a main domain |

The main domain acts as an umbrella. You can create many subdomains under it whenever needed.

### Why not just store all domains in the browser?

It seems simple: keep a list of domain to IP in the browser. It doesn't work, for two reasons:

- Too much data. There are 350+ million domains. The browser would become heavy and slow, and it can't know which sites you'll visit.
- IPs change. If a site moves hosting providers, its IP can change. Every browser in the world would need an update.

### Why not store it on one single server?

- A table of 350M+ entries (domain → IP) is too heavy for a single machine.
- It would be a single point of failure. If that machine broke, the entire internet would stop working, with no websites and no APIs.

So we need a distributed, well-designed system. That is DNS.
