<p align="center"><img src="logo.png" width="96" alt="Airfare Brain"></p>

# Airfare Brain MCP server

**The true cost of a flight, for AI assistants.** Bags, seats, priority boarding, check-in and payment fees on 32
airlines (Ryanair, easyJet, Wizz Air, Jet2, British Airways, Lufthansa, KLM, Air France, Iberia, Turkish, Finnair, SAS, Swiss, Austrian, Delta, United, Southwest, JetBlue and more), each price taken from the
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
<summary><strong>Claude Code (plugin)</strong></summary>

```
/plugin marketplace add jimiwalters-cmyk/airfare-brain-mcp
/plugin install airfare-brain@airfare-brain
```

Or add the server directly: `claude mcp add --transport http airfare-brain https://airfarebrain.com/mcp`
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

<!-- fee-pages:start (Scripts/public_readme.py) -->
## Fee pages

The same data as web pages, one per airline (checked bag, cabin bag, seats, with the date and the airline's own source):

[Aer Lingus](https://airfarebrain.com/aer-lingus/) · [Air Canada](https://airfarebrain.com/air-canada/) · [Air France](https://airfarebrain.com/air-france/) · [Alaska Airlines](https://airfarebrain.com/alaska-airlines/) · [American Airlines](https://airfarebrain.com/american-airlines/) · [Austrian Airlines](https://airfarebrain.com/austrian-airlines/) · [British Airways](https://airfarebrain.com/british-airways/) · [Delta Air Lines](https://airfarebrain.com/delta-air-lines/) · [easyJet](https://airfarebrain.com/easyjet/) · [Eurowings](https://airfarebrain.com/eurowings/) · [Finnair](https://airfarebrain.com/finnair/) · [Frontier Airlines](https://airfarebrain.com/frontier-airlines/) · [Iberia](https://airfarebrain.com/iberia/) · [Jet2](https://airfarebrain.com/jet2/) · [JetBlue](https://airfarebrain.com/jetblue/) · [KLM](https://airfarebrain.com/klm/) · [Lufthansa](https://airfarebrain.com/lufthansa/) · [Norwegian](https://airfarebrain.com/norwegian/) · [Pegasus](https://airfarebrain.com/pegasus/) · [Ryanair](https://airfarebrain.com/ryanair/) · [SAS](https://airfarebrain.com/sas/) · [Southwest Airlines](https://airfarebrain.com/southwest-airlines/) · [Swiss](https://airfarebrain.com/swiss/) · [TAP Air Portugal](https://airfarebrain.com/tap-air-portugal/) · [Transavia](https://airfarebrain.com/transavia/) · [Turkish Airlines](https://airfarebrain.com/turkish-airlines/) · [United Airlines](https://airfarebrain.com/united-airlines/) · [Virgin Atlantic](https://airfarebrain.com/virgin-atlantic/) · [Volotea](https://airfarebrain.com/volotea/) · [Vueling](https://airfarebrain.com/vueling/) · [WestJet](https://airfarebrain.com/westjet/) · [Wizz Air](https://airfarebrain.com/wizz-air/)

Compare all airlines: [checked bags](https://airfarebrain.com/compare/checked-bag-prices/) · [cabin bags](https://airfarebrain.com/compare/cabin-bag-prices/) · [seats](https://airfarebrain.com/compare/seat-prices/). Booking through Kiwi.com: [what it adds to bag prices](https://airfarebrain.com/booking-site-bag-fees/). Flights into [124 airports](https://airfarebrain.com/airports/) with the true cost and car hire there.
<!-- fee-pages:end -->

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
