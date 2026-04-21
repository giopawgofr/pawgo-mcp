# Pawgo MCP Server

**Real-time pet travel data for AI assistants.** Connect Claude, ChatGPT, or any MCP-compatible AI to Pawgo's database of airline pet policies and country import requirements.

Pawgo tracks **130+ airlines** and **100+ countries** with 200+ requirement fields per entity — cabin/cargo rules, breed restrictions, carrier dimensions, vaccination requirements, quarantine rules, health certificates, fees, and more.

## Why this exists

Pet travel information is scattered across airline PDFs, government websites, and outdated blog posts. Rules change constantly. Pet owners get conflicting answers and sometimes get turned away at the airport.

Pawgo's AI agent crawls official sources daily and structures everything into a single verified database. This MCP server makes that data available to any AI assistant, so when someone asks "Can I fly my French Bulldog on Delta?" — the AI gives an accurate, up-to-date answer.

## Quick start

### Install

```bash
pip install pawgo-mcp
```

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "pawgo": {
      "command": "pawgo-mcp",
      "args": []
    }
  }
}
```

Restart Claude Desktop. Ask: *"What's Air France's pet policy?"*

### With API key (full data access)

```json
{
  "mcpServers": {
    "pawgo": {
      "command": "pawgo-mcp",
      "args": [],
      "env": {
        "PAWGO_API_KEY": "your-key-here"
      }
    }
  }
}
```

Request a free API key at [info.pawgo.fr/developers](https://info.pawgo.fr/developers).

## Tools

| Tool | Description |
|------|-------------|
| `check_airline_policy` | Pet policy for a specific airline (cabin, cargo, breeds, fees) |
| `check_country_requirements` | Import/export requirements for a country (vaccines, quarantine, permits) |
| `compare_airlines` | Compare airlines by criteria: cabin, cargo, brachycephalic, cheapest |
| `search_countries` | Search countries: no_quarantine, easiest, titer_test |
| `get_coverage` | How many airlines and countries Pawgo tracks |

## Examples

Once connected, ask your AI assistant:

- *"Can I fly with my dog on Delta?"*
- *"What do I need to bring my cat to Japan?"*
- *"Which airlines allow French Bulldogs?"*
- *"What are the easiest countries for pet import?"*
- *"Does Australia require a quarantine for dogs?"*

## How it works

This MCP server calls the [Pawgo public API](https://info.pawgo.fr/api/v1/coverage) — no database access or credentials required. The API provides real-time data from Pawgo's continuously updated database.

For **personalized trip computation** — combining your specific pet, airline, origin country, destination country, and travel dates into a complete compliance checklist — visit [www.pawgo.fr](https://www.pawgo.fr).

## Environment variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PAWGO_API_BASE` | `https://info.pawgo.fr/api/v1` | API base URL |
| `PAWGO_API_KEY` | *(none)* | API key for full data access |
| `MCP_TRANSPORT` | `stdio` | Transport: `stdio` or `sse` |
| `MCP_PORT` | `8001` | Port for SSE transport |

## API

This server uses the Pawgo public REST API. You can also call it directly:

```bash
# Get Air France pet policy
curl https://info.pawgo.fr/api/v1/airlines/AF

# Get Japan import requirements
curl https://info.pawgo.fr/api/v1/countries/JP

# See all endpoints
curl https://info.pawgo.fr/api/v1/openapi.json
```

Full API docs: [info.pawgo.fr/developers](https://info.pawgo.fr/developers)

## Data coverage

- **130+ airlines** — cabin, checked, cargo policies for dogs and cats
- **100+ countries** — import/export requirements (microchip, rabies, titer test, health certificate, quarantine, import permit, breed restrictions)
- **Updated daily** by Pawgo's AI crawling agent
- **Completeness scored** — every record has a quality score (0-100%)

## Links

- **Pawgo** (trip planner): [www.pawgo.fr](https://www.pawgo.fr)
- **API docs**: [info.pawgo.fr/developers](https://info.pawgo.fr/developers)
- **Airline policies**: [info.pawgo.fr/airlines](https://info.pawgo.fr/airlines)
- **Country requirements**: [info.pawgo.fr/countries](https://info.pawgo.fr/countries)
- **Compare**: [info.pawgo.fr/compare](https://info.pawgo.fr/compare)

## License

MIT
