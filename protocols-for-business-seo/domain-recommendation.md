# Where the Protocols for Business site should live

4 October 2026 · Rafael Fernández · Companion to the [search and distribution strategy](README.md)

**Recommendation: serve the site from a folder on the Protocol Institute's own domain, `protocol-institute.org/business/`, and route that folder to the group's Cloudflare Pages project.** Register `protocolsforbusiness.com` only as a redirect to it, if it is available. If the Institute can't host a folder, use `business.protocol-institute.org`. A standalone .com is the third choice, not the first.

## The problem

The site lives at `npc.here.now/protocolvision/`: a subfolder of a shared staging host. Whatever links it earns build up on a domain the group doesn't control, robots.txt can't work there, and redirects are refresh pages rather than server 301s. The strategy's thesis is to borrow authority and travel through networks the group already belongs to. A domain choice either follows that thesis or works against it.

## What exists today

DNS lookups on 4 October 2026 show the following. A domain that resolves is registered; one that doesn't resolve may still be registered. Registration databases could not be reached from this environment.

| Domain | What it is | Host (from DNS) | Relevance |
| --- | --- | --- | --- |
| `npc.here.now/protocolvision/` | Current site, staging | here.now | To be retired; keep redirecting |
| `protocol-institute.org` | The Institute's site; already has a page for the group's meeting archive (`/sigs/sigpfb`) | Cloudflare | Parent organization, existing inbound links |
| `protocolized.summerofprotocols.com` | Protocolized magazine, where the group's essays appear | Cloudflare | Main source of the group's existing backlinks |
| `summerofprotocols.com` | Summer of Protocols, where the group began | Other host | Origin story, inbound links |
| `ai.protocolized.dev` | AI Capability Maturity Model and the Kitcraft workshop | Cloudflare | The group's guides already live on a separate domain |
| `rafael.fyi` | Rafael's site | Cloudflare | Personal, not for the group |
| `protocolvision.com` | Resolves to a parking-style address | AWS | Probably taken |
| `businessprotocols.com` | Resolves to a GoDaddy parking address | GoDaddy | Taken |
| `protocolsforbusiness.com`, `.org` | Do not resolve | — | Possibly available: check with a registrar |
| `protocolvision.org`, `businessprotocolmanagement.com` | Do not resolve | — | Possibly available |

## Options compared

| Option | Authority it starts with | Who controls deploys | Name fit | Effort | Verdict |
| --- | --- | --- | --- | --- | --- |
| `protocol-institute.org/business/` (folder) | Shares the Institute's links and history; every link the group earns also strengthens the Institute | Group deploys its own Pages project; the Institute owns one route rule | Matches "a research group of the Protocol Institute", already in every page footer | One Cloudflare Worker route on the Institute's zone | **Recommended** |
| `business.protocol-institute.org` (subdomain) | Partial: Google may treat it as a separate site, but the brand and cross-links carry | Group, via a DNS record the Institute adds | Same | One DNS record | Fallback |
| `protocolsforbusiness.com` (standalone) | None: starts from zero links | Group alone | Exact group name, no Institute link in the address | Purchase, renewals, a separate Search Console property | Third choice; useful as a redirect |
| `protocolvision.com` / `.org` | None | Group | "Protocol vision" is the capability, not the group, and its searches return crypto and machine-vision products | Purchase, if available | Not recommended |
| A `protocolized.dev` subdomain | Little | Group | Ties the group to the magazine, not the Institute | DNS record | Not recommended |

Why the folder wins:

1. **It follows the strategy.** Section 2 of the strategy argues that a new term earns no links and that the group should borrow existing authority. A folder on the Institute's domain borrows it directly; a new .com builds from zero.
2. **Links pool in both directions.** Reading notes that earn links from engineers and safety writers also lift the Institute's domain. That's a reason for the Institute to say yes.
3. **The name already says it.** Every page footer reads "Protocols for Business, a research group of the Protocol Institute", and the header reads "Protocol Institute – Business". The address would match what the page claims.
4. **It is cheap on Cloudflare.** Both the Institute's domain and the group's sign-up Worker run on Cloudflare. A Worker route on `protocol-institute.org/business/*` can serve the group's Pages project, so the group keeps its own repo, builds and deploys.

## Why `/business/` and not another path

- **Short and readable**, and it matches the header ("Protocol Institute – Business").
- **It survives renames.** `/sigs/` is out of date now that the group is a research group; a path without the group type won't need another move.
- **It leaves room for other groups** under the same pattern, such as `/robotics/`.

If the Institute prefers a path that names group type, `protocol-institute.org/research/business/` works too. Avoid `/protocolvision/`: it names the capability, not the group.

## Steps

1. **Ask the Institute** (Timber, as director) for the `/business/` route on `protocol-institute.org`, and agree who can change it.
2. **Move hosting to Cloudflare Pages** from the `sig-p4b` repo, and add the Worker route so `protocol-institute.org/business/*` serves it.
3. **Set `"site": "https://protocol-institute.org/business/"` in `config.json`** and follow "Search and the move to a new domain" in the `sig-p4b` README. Robots.txt then lives with the Institute's root file: add the group's sitemap line there.
4. **Redirect** `npc.here.now/protocolvision/*` and the Institute's old `/sigs/sigpfb` page to the matching new paths, for at least a year.
5. **Add the folder as a URL-prefix property in Google Search Console** and in Bing Webmaster Tools, and submit the sitemap.
6. **Optionally register `protocolsforbusiness.com`** and 301 it to the folder, so the name is protected and easy to say aloud.

## Assumptions to pressure-test

- [ ] **The Institute will host a folder.** It is becoming a Canada-based nonprofit and raising 2027 support. Its team may prefer a subdomain, or prefer that groups keep their own domains. Ask before buying anything.
- [ ] **The Institute's domain is on a Cloudflare account it can add a Worker route to.** DNS shows Cloudflare's network, not who holds the account.
- [ ] **Availability is unverified.** `protocolsforbusiness.com` didn't resolve, which doesn't prove it's unregistered. Check with a registrar.
- [ ] **Authority gain is directional, not measured.** Google has said subdomains and folders can both rank well. The case for the folder rests on pooling links and on the group's small size, not on a guaranteed ranking effect.
- [ ] **The group may outgrow the Institute.** If the group might later spin out, a standalone domain avoids a second move. The redirect domain in step 6 keeps that option open.
- [ ] **A .com was the plan.** For a research group inside a nonprofit, `.org` or the Institute's domain reads more naturally than `.com`. Keep the .com only as the redirect.
