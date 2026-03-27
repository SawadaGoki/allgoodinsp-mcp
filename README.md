# AllGoodInsp MCP Server

A curated design reference database for AI agents. Retrieve structured design data from 736+ websites — real CSS values, typography specs, color palettes, and design rationale — to generate better web designs.

Instead of generating from generic prompts, your AI retrieves actual design decisions from quality sites and synthesizes them into code-ready specifications.

## Quick Start

### Claude Desktop / Claude Code / Cursor

Add to your MCP configuration:

```json
{
  "mcpServers": {
    "allgoodinsp": {
      "url": "https://mcp.allgoodinsp.com/mcp"
    }
  }
}
```

**Configuration file locations:**

| Client | Path |
|--------|------|
| Claude Desktop (macOS) | `~/Library/Application Support/Claude/claude_desktop_config.json` |
| Claude Desktop (Windows) | `%APPDATA%\Claude\claude_desktop_config.json` |
| Claude Code | `~/.claude.json` or project `.mcp.json` |
| Cursor | `.cursor/mcp.json` in your project |

On first connection, you'll be prompted to authenticate via Google OAuth through your browser.

### API Key Authentication

For server-to-server or CI/CD use, generate an API key at [allgoodinsp.com/account](https://allgoodinsp.com/account) and pass it as a Bearer token:

```
Authorization: Bearer agi_your_key_here
```

## Tools

### `extract_essence` — Primary tool

Synthesize 2-5 site references into a code-ready design brief. Returns CSS variables, color palette, typography scale, spacing system, section structure, and design rules with fixed/explorable boundaries.

```
extract_essence({
  site_ids: ["stripe-com", "linear-app", "vercel-com"],
  brief: "SaaS landing page for a developer tool, confident and minimal"
})
```

### `search_sites`

Semantic search across all references by mood, purpose, or description. Uses 3-axis search (purpose + mood + contrast diversity) to return varied results.

```
search_sites({ query: "warm editorial magazine layout" })
search_sites({ query: "bold fintech landing page", category: "software-saas" })
```

### `get_site`

Retrieve the full design analysis for a specific site — color palette, typography, sections, components with CSS values and rationale.

```
get_site({ site_id: "stripe-com" })
get_site({ site_id: "stripe-com", detail: "full" })
```

### `search_by_component`

Find sites by specific design elements. Searches across all components in all references.

```
search_by_component({ query: "hero with video background" })
search_by_component({ query: "pricing table with toggle" })
```

### `get_methodology`

Access the design methodology — universal principles, craft guidelines, recurring patterns, and information architecture.

```
get_methodology({ layers: ["principles", "patterns"] })
```

### `get_principles`

Design principles for specific domains.

```
get_principles({ category: "typography" })
get_principles({ category: "color" })
```

Available categories: `typography`, `layout`, `color`, `motion`, `ia`

### `get_patterns`

Recurring technique combinations distilled from the collection, with evidence from multiple sites.

```
get_patterns()
```

### `get_reference_guide`

Guide for reading and combining design references effectively.

### `get_workflow`

Autonomous workflow for AI agents building design systems from references.

### `self_review`

Post-implementation quality checklist for design patterns, anti-patterns, craft quality, and information architecture.

## What's in the data

Each reference contains structured design decisions from a real website:

- **Color palette** — background, text primary/secondary, CTA, accent (with hex values and rationale)
- **Typography** — font families, weights, sizes, line-heights, letter-spacing for headings, body, nav, CTA
- **Convention breaks** — intentional violations of design principles, with scope and rationale
- **Sections** — hero, navigation, content, CTA, footer — each with dominant design decisions
- **Components** — individual elements with CSS values, principle references, and "why" explanations

### Three-layer knowledge system

| Layer | Description | Count |
|-------|-------------|-------|
| **Principles** | Universal design truths (typography, layout, color, motion, IA) | 30+ |
| **Patterns** | Recurring technique combinations observed across multiple sites | 30+ |
| **References** | Per-site structured JSON with design decisions and CSS values | 736+ |

### Categories

Agency, E-Commerce, Consulting, Software/SaaS, Portfolio, Food & Beverage, Hospitality, Education, Health & Wellness, Media/Editorial, Deep-Tech, Architecture, Business/Finance, Recruitment, and more.

### Coverage

736+ sites across 20+ countries, with 62% Japan and 26% US coverage.

## REST API

For programmatic access outside MCP, a REST API is also available.

**Base URL:** `https://api.allgoodinsp.com/v1`

| Endpoint | Description |
|----------|-------------|
| `GET /sites` | List sites (filterable by category, country, region) |
| `GET /sites/:site_id` | Full design analysis for a site |
| `GET /search?q=` | Semantic search |
| `GET /taxonomy` | Categories, countries, regions with counts |
| `GET /screenshots/:site_id` | Site screenshot |

Authentication required for higher rate limits. Generate an API key at [allgoodinsp.com/account](https://allgoodinsp.com/account).

## Links

- **Gallery:** [allgoodinsp.com](https://allgoodinsp.com)
- **MCP Endpoint:** `https://mcp.allgoodinsp.com/mcp`
- **REST API:** `https://api.allgoodinsp.com/v1`
- **MCP Docs:** [allgoodinsp.com/docs/mcp](https://allgoodinsp.com/docs/mcp)
- **API Docs:** [allgoodinsp.com/docs/api](https://allgoodinsp.com/docs/api)

## License

MIT
