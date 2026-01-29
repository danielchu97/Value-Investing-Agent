[English](README.md) | [中文](README_CN.md)

# Value Investing Agent

An AI-powered MCP server for value investors. Analyze stocks using principles from Benjamin Graham and Warren Buffett. Every value investor deserves their own AI agent.

> *"Price is what you pay. Value is what you get."* - Warren Buffett

[![npm version](https://img.shields.io/npm/v/value-investing-agent.svg)](https://www.npmjs.com/package/value-investing-agent)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)](https://nodejs.org/)
[![MCP](https://img.shields.io/badge/MCP-Compatible-blue)](https://modelcontextprotocol.io/)

## Disclaimer

**This tool is for educational and research purposes only. It does not constitute investment advice. Investing involves risks, including the potential loss of principal. The author is not responsible for any investment decisions made based on this tool.**

## Features

- 📊 **Real-time Stock Data** - Quotes, financials, and company profiles
- 🧮 **Intrinsic Value Calculation** - DCF model and Graham Number
- 🏰 **Moat Analysis** - Evaluate competitive advantages
- 📰 **News Aggregation** - Stay informed on your watchlist
- 📝 **Report Generation** - Daily summaries and deep analysis reports
- 🔌 **Pluggable Data Sources** - Easy to add your own data providers

## Quick Start

### Prerequisites

- Node.js >= 18.0.0
- Any MCP-compatible client (Claude Desktop, Claude Code, or your own application)

> **Note:** This is a standalone MCP server that can run on Windows, macOS, or Linux. It can be used with any application that supports the [Model Context Protocol](https://modelcontextprotocol.io/), not just Claude products.

### Installation

#### Option 1: npx (Recommended)

No installation required:

```bash
npx value-investing-agent
```

Or configure in your MCP client:

```json
{
  "mcpServers": {
    "value-investing-agent": {
      "command": "npx",
      "args": ["-y", "value-investing-agent"]
    }
  }
}
```

#### Option 2: Global Install

```bash
npm install -g value-investing-agent
```

Configure MCP:

```json
{
  "mcpServers": {
    "value-investing-agent": {
      "command": "value-investing-agent"
    }
  }
}
```

#### Option 3: From Source

```bash
git clone https://github.com/danielchu97/Value-Investing-Agent.git
cd Value-Investing-Agent
npm install
npm run build
```

Configure MCP:

```json
{
  "mcpServers": {
    "value-investing-agent": {
      "command": "node",
      "args": ["/path/to/value-investing-agent/dist/index.js"]
    }
  }
}
```

### Configuration Files

**Claude Desktop:**
- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

## Usage

### Get Stock Quote

```
"Get me the current quote for Apple"
"What's the price of MSFT?"
```

### Analyze Intrinsic Value

```
"Calculate the intrinsic value of AAPL"
"What is Amazon's fair value using DCF?"
```

### Evaluate Economic Moat

```
"Analyze the competitive moat of Coca-Cola"
"Does Microsoft have a wide moat?"
```

### Manage Watchlist

```
"Add GOOGL to my watchlist in the Technology group"
"Show my watchlist"
"Remove TSLA from watchlist"
```

### Generate Reports

```
"Generate a daily report for my watchlist"
"Create a detailed analysis report for Berkshire Hathaway"
```

## Available Tools

| Tool | Description |
|------|-------------|
| `get_stock_quote` | Get real-time stock quote and metrics |
| `get_financials` | Fetch financial statements (income, balance, cash flow) |
| `calculate_intrinsic_value` | DCF and Graham valuation with margin of safety |
| `analyze_moat` | Evaluate competitive advantages |
| `get_news` | Get stock-related news articles |
| `manage_watchlist` | Manage your personal stock watchlist |
| `generate_daily_report` | Daily summary of watchlist stocks |
| `generate_stock_report` | Comprehensive value investing analysis |
| `set_provider` | Switch data provider |
| `list_providers` | List available data providers |

## Data Providers

The plugin architecture allows you to add your own data sources. See [Custom Provider Guide](docs/custom-provider.md).

### Built-in Providers

| Provider | API Key | Rate Limit | Best For |
|----------|---------|------------|----------|
| **yahoo-finance** (default) | Not required | Limited (may hit 429 errors) | Quick testing |
| **finnhub** | Required (free) | 60 calls/min | Production use |
| **alpha-vantage** | Required (free) | 5 calls/min | Basic data needs |

### Configuring API Keys

**Finnhub** (Recommended for reliable access):
1. Get free API key at [finnhub.io/register](https://finnhub.io/register)
2. Set environment variable:
   ```bash
   export FINNHUB_API_KEY=your_api_key_here
   ```
   Or in Claude Desktop config:
   ```json
   {
     "mcpServers": {
       "value-investing-agent": {
         "command": "npx",
         "args": ["-y", "value-investing-agent"],
         "env": {
           "FINNHUB_API_KEY": "your_api_key_here"
         }
       }
     }
   }
   ```

**Alpha Vantage**:
1. Get free API key at [alphavantage.co](https://www.alphavantage.co/support/#api-key)
2. Set environment variable: `ALPHA_VANTAGE_API_KEY=your_key`

### Switching Providers

```
"Switch to finnhub provider"
"Use alpha-vantage for data"
"List available providers"
```

### Adding a Custom Provider

1. Copy `src/providers/provider-template.ts`
2. Implement the `DataProvider` interface
3. Register in `src/providers/index.ts`

```typescript
import { MyProvider } from './my-provider';
registerProvider('my-provider', (config) => new MyProvider(config));
```

## Value Investing Principles

This tool is built on timeless investment principles:

### 1. Intrinsic Value
A company's true worth based on future cash flows, not market price.

### 2. Margin of Safety
Buy only when price is significantly below intrinsic value (25%+ discount).

### 3. Economic Moat
Seek durable competitive advantages that protect profits.

### 4. Circle of Competence
Only invest in businesses you understand.

### 5. Mr. Market
Use market emotions as opportunities, don't be ruled by them.

## Key Metrics

### Valuation
- P/E Ratio: < 15 (undervalued)
- P/B Ratio: < 1.5 (undervalued)
- Graham Number: Price ceiling for defensive investors

### Profitability
- ROE: > 15% (excellent)
- Gross Margin: > 40% (pricing power)
- Net Margin: > 10% (efficient)

### Safety
- Current Ratio: > 1.5 (liquid)
- Debt/Equity: < 1.0 (conservative)
- Interest Coverage: > 5x (safe)

## Development

```bash
# Install dependencies
npm install

# Build
npm run build

# Development mode (watch)
npm run dev

# Run tests
npm test

# Lint
npm run lint
```

## Project Structure

```
value-investing-agent/
├── src/
│   ├── index.ts              # Entry point
│   ├── server.ts             # MCP server
│   ├── providers/            # Data providers
│   ├── tools/                # MCP tools
│   ├── analysis/             # Analysis engine
│   ├── utils/                # Utilities
│   ├── config/               # Configuration
│   └── types/                # TypeScript types
├── skills/                   # Claude skills
├── data/                     # Local data (watchlist, cache)
├── docs/                     # Documentation
└── tests/                    # Test files
```

## Contributing

Contributions are welcome! Please read our contributing guidelines before submitting PRs.

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests
5. Submit a pull request

## License

MIT License - see [LICENSE](LICENSE) for details.

## Acknowledgments

This project is inspired by the investment wisdom of:

- **Benjamin Graham** - *The Intelligent Investor*, *Security Analysis*
- **Warren Buffett** - Berkshire Hathaway Letters to Shareholders
- **Charlie Munger** - *Poor Charlie's Almanack*

## Resources

- [The Intelligent Investor](https://www.amazon.com/Intelligent-Investor-Definitive-Investing-Essentials/dp/0060555661) by Benjamin Graham
- [Berkshire Hathaway Letters](https://www.berkshirehathaway.com/letters/letters.html)
- [Value Investing Guide](docs/value-investing-guide.md)

---

**Remember:** *"The stock market is designed to transfer money from the active to the patient."* - Warren Buffett
