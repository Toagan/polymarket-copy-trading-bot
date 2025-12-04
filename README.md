# Polymarket Copy Trading Bot

> Automated copy trading bot for Polymarket that mirrors trades from top performers with intelligent position sizing and real-time execution.

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](LICENSE)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)](https://nodejs.org/)

## Overview

The Polymarket Copy Trading Bot automatically replicates trades from successful Polymarket traders to your wallet. It monitors trader activity 24/7, calculates proportional position sizes based on your capital, and executes matching orders in real-time.

### How It Works

<<<<<<< HEAD
1. **Select Traders** - Choose top performers from [Polymarket leaderboard](https://polymarket.com/leaderboard) or [Predictfolio](https://predictfolio.com)
2. **Monitor Activity** - Bot continuously watches for new positions opened by selected traders using Polymarket Data API
3. **Calculate Size** - Automatically scales trades based on your balance vs. trader's balance
4. **Execute Orders** - Places matching orders on Polymarket using your wallet
5. **Track Performance** - Maintains complete trade history in MongoDB

## Quick Start

### Prerequisites

- Node.js v18+
- MongoDB database ([MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register) free tier works)
- Polygon wallet with USDC and POL/MATIC for gas
- RPC endpoint ([Infura](https://infura.io) or [Alchemy](https://www.alchemy.com) free tier)

### Installation

```bash
# Clone repository
git clone <repository-url>
cd polymarket-copytrading-bot

# Install dependencies
npm install

# Run interactive setup wizard
npm run setup

# Build and start
npm run build
npm run health-check  # Verify configuration
npm start             # Start trading
```

**📖 For detailed setup instructions, see [Getting Started Guide](./GETTING_STARTED.md)**

## Features

- **Multi-Trader Support** - Track and copy trades from multiple traders simultaneously
- **Smart Position Sizing** - Automatically adjusts trade sizes based on your capital
- **Tiered Multipliers** - Apply different multipliers based on trade size
- **Position Tracking** - Accurately tracks purchases and sells even after balance changes
- **Trade Aggregation** - Combines multiple small trades into larger executable orders
- **Real-time Execution** - Monitors trades every second and executes instantly
- **MongoDB Integration** - Persistent storage of all trades and positions
- **Price Protection** - Built-in slippage checks to avoid unfavorable fills

### Monitoring Method

The bot currently uses the **Polymarket Data API** to monitor trader activity and detect new positions. The monitoring system polls trader positions at configurable intervals (default: 1 second) to ensure timely trade detection and execution.

**🚀 Upcoming:** The next version will migrate to **RTDS (Real-Time Data Stream)** for even faster trade detection with lower latency and reduced API load. This will enable near-instantaneous trade replication as positions are opened.

## Configuration

### Essential Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `USER_ADDRESSES` | Traders to copy (comma-separated) | `'0xABC..., 0xDEF...'` |
| `PROXY_WALLET` | Your Polygon wallet address | `'0x123...'` |
| `PRIVATE_KEY` | Wallet private key (no 0x prefix) | `'abc123...'` |
| `MONGO_URI` | MongoDB connection string | `'mongodb+srv://...'` |
| `RPC_URL` | Polygon RPC endpoint | `'https://polygon...'` |
| `TRADE_MULTIPLIER` | Position size multiplier (default: 1.0) | `2.0` |
| `FETCH_INTERVAL` | Check interval in seconds (default: 1) | `1` |

### Finding Traders

1. Visit [Polymarket Leaderboard](https://polymarket.com/leaderboard)
2. Look for traders with positive P&L, win rate >55%, and active trading history
3. Verify detailed stats on [Predictfolio](https://predictfolio.com)
4. Add wallet addresses to `USER_ADDRESSES`

**📖 For complete configuration guide, see [Quick Start](./docs/QUICK_START.md)**

## Docker Deployment

Deploy with Docker Compose for a production-ready setup:

```bash
# Configure and start
cp .env.example .env
docker-compose up -d

# View logs
docker-compose logs -f polymarket
```

**📖 [Complete Docker Guide →](./docs/DOCKER.md)**

## Safety & Risk Management

⚠️ **Important Disclaimers:**

- **Use at your own risk** - This bot executes real trades with real money
- **Start small** - Test with minimal funds before scaling up
- **Diversify** - Don't copy just one trader; track multiple strategies
- **Monitor regularly** - Check bot logs daily to ensure proper execution
- **No guarantees** - Past performance doesn't guarantee future results

### Best Practices

1. Use a dedicated wallet separate from your main funds
2. Only allocate capital you can afford to lose
3. Research traders thoroughly before copying
4. Set up monitoring and alerts
5. Know how to stop the bot quickly (Ctrl+C)

## Documentation

### Getting Started
- **[🚀 Getting Started Guide](./GETTING_STARTED.md)** - Complete beginner's guide
- **[⚡ Quick Start](./docs/QUICK_START.md)** - Fast setup for experienced users

### Advanced Guides
- **[🐳 Docker Deployment](./docs/DOCKER.md)** - Container deployment
- **[👥 Multi-Trader Guide](./docs/MULTI_TRADER_GUIDE.md)** - Copy multiple traders
- **[📍 Position Tracking](./docs/POSITION_TRACKING.md)** - How tracking works
- **[💰 Funding Guide](./docs/FUNDING_GUIDE.md)** - Wallet funding instructions

### Testing & Analysis
- **[🧪 Simulation Guide](./docs/SIMULATION_GUIDE.md)** - Backtest strategies
- **[🔬 Simulation Runner](./docs/SIMULATION_RUNNER_GUIDE.md)** - Advanced backtesting

## Troubleshooting

### Common Issues

**Missing environment variables** → Run `npm run setup` to create `.env` file

**MongoDB connection failed** → Verify `MONGO_URI`, whitelist IP in MongoDB Atlas

**Bot not detecting trades** → Verify trader addresses and check recent activity

**Insufficient balance** → Add USDC to wallet and ensure POL/MATIC for gas fees

**Run health check:** `npm run health-check`

**📖 For detailed troubleshooting, see [Quick Start Guide](./docs/QUICK_START.md)**

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

ISC License - See [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built on [Polymarket CLOB Client](https://github.com/Polymarket/clob-client)
- Uses [Predictfolio](https://predictfolio.com) for trader analytics
- Powered by Polygon network
=======
## Overview

Automated trading bot that monitors a selected trader's activity on Polymarket and executes matching trades in your account with proportional position sizing.

**Key Features:**
- 🔄 Real-time trade monitoring and execution
- 📊 Proportional position sizing based on account balance
- 🛡️ Price validation and retry mechanisms
- 💾 Persistent trade history in MongoDB

## Prerequisites

- Node.js v16+ and npm
- MongoDB (local or Atlas)
- Polymarket account with funded wallet
- Polygon RPC access (Infura, Alchemy, etc.)

## Quick Start

### 1. Clone & Install

```bash
git clone https://github.com/vladmeer/polymarket-copy-trading-bot.git
cd polymarket-copy-trading-bot
npm install
```

### 2. Configure Environment

Create `.env` file:

```env
# Required
USER_ADDRESS=0xYourTargetTraderWalletAddress
PROXY_WALLET=0xYourPolymarketWalletAddress
PRIVATE_KEY=YourWalletPrivateKey
CLOB_HTTP_URL=https://clob.polymarket.com/
CLOB_WS_URL=wss://ws-subscriptions-clob.polymarket.com/ws
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/database
RPC_URL=https://polygon-mainnet.infura.io/v3/YOUR_INFURA_KEY
USDC_CONTRACT_ADDRESS=0x2791Bca1f2de4661ED88A30C99A7a9449Aa84174

# Optional (defaults shown)
FETCH_INTERVAL=1
TOO_OLD_TIMESTAMP=24
RETRY_LIMIT=3
```

### 3. Build & Run

```bash
npm run build
npm run start
```

For development: `npm run dev`

## Configuration

| Variable | Description | Required |
|----------|-------------|----------|
| `USER_ADDRESS` | Target trader wallet address | ✅ |
| `PROXY_WALLET` | Your Polymarket wallet address | ✅ |
| `PRIVATE_KEY` | Your wallet private key | ✅ |
| `CLOB_HTTP_URL` | Polymarket CLOB API endpoint | ✅ |
| `MONGO_URI` | MongoDB connection string | ✅ |
| `RPC_URL` | Polygon RPC endpoint | ✅ |
| `USDC_CONTRACT_ADDRESS` | USDC contract on Polygon | ✅ |
| `FETCH_INTERVAL` | Polling interval (seconds) | ❌ |
| `TOO_OLD_TIMESTAMP` | Max trade age (hours) | ❌ |
| `RETRY_LIMIT` | Max retry attempts | ❌ |

## How It Works

1. **Monitor** → Polls Polymarket API for target trader's trades
2. **Store** → Saves trades to MongoDB
3. **Analyze** → Compares positions and balances
4. **Execute** → Places proportional orders via CLOB API
5. **Retry** → Handles failed trades automatically

**Trading Strategies:**
- **Buy**: Proportional sizing based on balance ratio with price validation
- **Sell**: Proportional sell based on position ratios
- **Merge**: Closes positions when target trader merges

## Deployment

**Recommended VPS**: [TradingVPS.io](https://app.tradingvps.io/link.php?id=11) (Germany location for low latency)

**Production Setup:**
```bash
npm install -g pm2
pm2 start dist/index.js --name polymarket-bot
pm2 save
pm2 startup
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Bot not detecting trades | Verify `USER_ADDRESS` and MongoDB connection |
| Trades not executing | Check `PRIVATE_KEY`, wallet balance, and RPC endpoint |
| MongoDB errors | Verify `MONGO_URI` and network connectivity |
| API errors | Check `CLOB_HTTP_URL` and wallet configuration |

## Security

- ✅ Never commit `.env` file
- ✅ Store private keys securely
- ✅ Use authenticated MongoDB connections
- ✅ Keep dependencies updated

## Support

- **Issues**: [GitHub Issues](https://github.com/vladmeer/polymarket-copy-trading-bot/issues)
- **Telegram**: [@vladmeer67](https://t.me/vladmeer67)
- **Documentation**: See `Polymarket Copy Trading Bot Documentation.pdf`

## Contributing

Contributions welcome! Fork, create a feature branch, and submit a PR.

```bash
npm run lint      # Check code
npm run lint:fix  # Fix issues
npm run format    # Format code
```

## Disclaimer

This software is provided "as is" without warranty. Trading involves substantial risk. Use at your own risk.

## License

ISC License
>>>>>>> 89a8d785f76c69d9811e749b30a22bd6838a7f6d

---

**Disclaimer:** This software is for educational purposes only. Trading involves risk of loss. The developers are not responsible for any financial losses incurred while using this bot.

<<<<<<< HEAD
**Support:** For questions or issues, contact via Telegram: [@Vladmeer](https://t.me/vladmeer67)
=======
**Made with ❤️ for the Polymarket community**

⭐ Star this repo if you find it helpful!

</div>
>>>>>>> 89a8d785f76c69d9811e749b30a22bd6838a7f6d
