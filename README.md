<p align="center"><img src="logo.png" width="96" alt="Airfare Brain"></p>

# Airfare Brain MCP server

**The true cost of a flight, for AI assistants.** Bags, seats, priority boarding, check-in and payment fees on 25
airlines (Ryanair, easyJet, Wizz Air, Jet2, British Airways, Lufthansa, KLM, Air France, Iberia, Turkish, TAP, Delta, United and more), each price taken from the
airline's own pages, with the source and the date it was checked.

Free. No API key. No login. Read-only.

**MCP endpoint (streamable HTTP):**

```
https://airfarebrain.com/mcp
```

Listed in the official [MCP Registry](https://registry.modelcontextprotocol.io) as `com.airfarebrain/airfare-brain`.
Website: [airfarebrain.com](https://airfarebrain.com) · Fee data: [airfarebrain.com/fees](https://airfarebrain.com/fees/) ·
For AI: [llms.txt](https://airfarebrain.com/llms.txt)

## Why it exists

The fare a flight search shows is not what the trip costs. A cabin bag, a checked bag, a seat next to someone you know,
checking in at the airport or paying by card can each add more than the fare itself, and the price goes up if you add
them later or at the airport. Airfare Brain reads each airline's published fee pages, records every price with its
source and date, and answers with the numbers, so an assistant can say what a flight will really cost.

## Tools

| Tool | What it answers |
|---|---|
| `get_capabilities` | What is covered, how fees are researched and dated, what it does not do (no live fares, no booking) |
| `list_airlines` | Every airline with a fee table: name, IATA code, the date its fees were checked, its page |
| `airline_fees` | One airline's extras (bags, seats, priority, check-in, changes, payment): price range, when bought (at booking / later / at the airport), source URL, date checked |
| `true_cost` | Fare + the extras the person chooses, for the whole party and each flight, with what it costs if added later or at the airport |
| `trip_at_airport` | The whole trip into one airport: the flight's extras on an airline AND what car hire there really costs (Car Rental Brain's measured median per day), dated and linked |

Ranges are shown exactly as the airline publishes them. A fee the airline does not publish is said to be unknown,
never counted as free. Figures from a third party (only where the airline publishes none) are labelled "reported".

## Example questions

- "I found a Ryanair flight for €39. What will it cost with a cabin bag and a 20kg bag, return?"
- "Is easyJet or Wizz Air cheaper for two people with one checked bag between them?"
- "What does Jet2 charge to choose a seat?"
- "How much more is a bag at the airport than online on Wizz Air?"
- "Does British Airways' Basic fare include a cabin bag?"
- "Flying Ryanair into Malaga for a week with a 20kg bag and a hire car: what will it all cost?"

## Connect

<details>
<summary><strong>Claude (claude.ai / Claude Desktop)</strong></summary>

Settings → Connectors → Add custom connector → URL `https://airfarebrain.com/mcp`.

Or in `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "airfare-brain": { "url": "https://airfarebrain.com/mcp" }
  }
}
```
</details>

<details>
<summary><strong>ChatGPT</strong></summary>

Settings → Apps & Connectors → Advanced → Developer mode → Create → MCP server URL
`https://airfarebrain.com/mcp`, authentication: none.
</details>

<details>
<summary><strong>Cursor / Windsurf / Cline / VS Code</strong></summary>

```json
{
  "mcpServers": {
    "airfare-brain": { "url": "https://airfarebrain.com/mcp" }
  }
}
```
</details>

<details>
<summary><strong>Stdio-only clients</strong></summary>

```bash
npx mcp-remote https://airfarebrain.com/mcp
```
</details>

<details>
<summary><strong>Plain JSON</strong></summary>

All fee tables in one file: [airfarebrain.com/data/fees.json](https://airfarebrain.com/data/fees.json).
</details>

## How the numbers are made

Each airline's fee pages are read by hand, every value is stored with the page it came from, a short quote and the
date, and each table is re-checked monthly (a table past its re-check date is flagged on the site). Travellers can
report what they actually paid; those reports are checked against the tables.

## Sister tool

For car hire at the airport you land at: [Car Rental Brain](https://github.com/jimiwalters-cmyk/car-rental-brain-mcp)
(`https://app.carrentalbrain.com/mcp`).

## Affiliate disclosure

The MCP tools return fee data only, with no booking links. The airfarebrain.com website's flight search links to
Kiwi.com through its affiliate programme, and Airfare Brain may earn a small commission at no cost to the person
booking.

## Privacy

The tools take no personal data and need no account. Privacy policy:
[airfarebrain.com/privacy](https://airfarebrain.com/privacy/).

## Contact

hello@airfarebrain.com
