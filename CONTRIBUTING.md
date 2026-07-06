# Contributing

Thanks for helping improve the **OSINT & Threat Intelligence Toolkit**. This project is a curated, *verifiable* catalog — the single most important rule is that **every number is verifiable, none are hand-typed.**

## How to propose adding or updating a tool

1. **Open an issue** describing the tool (or the update), or go straight to a **pull request**.
2. Make sure the tool meets the [inclusion criteria](#inclusion-criteria) below.
3. Update **both** the embedded data in `index.html` **and** `tools.json` so they stay in sync (see [Data model](#data-model)).
4. In your issue/PR, paste the `gh api` output you used to verify the metadata so a reviewer can confirm it.

## Inclusion criteria

A tool qualifies if it is:

- **Genuinely open-source** — it has a real open-source license (or is clearly source-available and community-usable).
- **Hosted on GitHub** — so its metadata can be verified through the GitHub REST API.
- **Relevant** to OSINT, reconnaissance, threat intelligence, malware analysis, detection engineering, DFIR/SOC operations, or intel enrichment/orchestration.
- **Actively useful** — maintained or still widely relied upon.

## Metadata must be verifiable

All metadata — **stars, primary language, license, and last-updated date** — must be verifiable via:

```bash
gh api repos/OWNER/NAME
```

Use the API response fields directly:

- `stargazers_count` → `stars`
- `language` → `language`
- `license.spdx_id` → `license` (use `—`/none when the API returns no SPDX license)
- `pushed_at` → `lastPushed` (date portion, `YYYY-MM-DD`)

**Do not hand-type numbers or estimate them.** If you can't verify a value from the API, don't submit it.

## Categories

There are 8 categories, and we aim for a roughly **even distribution** across them (currently 6–8 tools each):

1. **OSINT Recon & Footprinting**
2. **Username, People & Email Enumeration**
3. **Network & Attack-Surface Mapping**
4. **Threat Intelligence Platforms (TIP)**
5. **Malware Analysis & Sandboxing**
6. **Detection Engineering & Hunting**
7. **SOC, IR & Case Management**
8. **Feeds, Enrichment & Orchestration**

When proposing a new tool, prefer categories that are under-represented, and pick the single best-fitting category.

## Data model

Each tool is an object with these fields:

| Field | Description |
| --- | --- |
| `name` | Display name of the tool |
| `repo` | `OWNER/NAME` GitHub slug |
| `category` | One of the 8 categories above |
| `stars` | `stargazers_count` from the GitHub API |
| `language` | Primary `language` from the GitHub API |
| `license` | SPDX license id (or none/`—` if unrecognized) |
| `lastPushed` | `pushed_at` date (`YYYY-MM-DD`) |
| `description` | Short one-line summary |
| `keyFeatures` | Array of 3–4 concise bullet strings |

**`index.html` embeds this data** (in the `DATA` object) and drives the live dashboard, while **`tools.json` mirrors it** as the machine-readable source of truth. A change to one must be reflected in the other. `tools.json` is pretty-printed (2-space indent) and sorted by category (in the order above), then by stars descending.

## Verification date

When you refresh metadata for a batch of tools, note the date and keep the `verified-*` badge and the Methodology date in `README.md` consistent with the freshest full re-verification.
