# social-trading-signals

[![License: MIT](https://img.shields.io/github/license/1322monitors/social-trading-signals?style=flat-square&color=blue)](LICENSE) [![Last commit](https://img.shields.io/github/last-commit/1322monitors/social-trading-signals?style=flat-square)](https://github.com/1322monitors/social-trading-signals/commits) [![CI](https://github.com/1322monitors/social-trading-signals/actions/workflows/ci.yml/badge.svg)](https://github.com/1322monitors/social-trading-signals/actions/workflows/ci.yml) [![Built for 1322.io](https://img.shields.io/badge/built%20for-1322.io-3b82f6?style=flat-square)](https://1322.io) [![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](https://github.com/1322monitors/social-trading-signals/pulls)

<p align="center">
  <a href="https://1322.io"><img src="assets/demo.gif" alt="1322 real-time feed demo" width="680"></a>
</p>
<p align="center"><sub>▶ The <a href="https://1322.io">1322</a> dashboard these clients stream from — API keys, WebSocket &amp; REST endpoints, live feed.</sub></p>

Pipe real-time social posts into your trading bot: a tiny Python harness that consumes a 1322 WebSocket feed from X (Twitter), Truth Social or Binance Square (one feed per source) and hands each event to your strategy function as it lands, so the bot reacts when an account posts, not on the next poll. It runs against the 1322 feed (X typically 150-250ms; Truth Social 150-250ms typical; Binance Square sub-second, coin pairs parsed); the consumer is generic. Maintained by the 1322 team.

Your bot is only as fast as its slowest input. Polling a REST endpoint caps you
at the poll interval and burns rate limits. A persistent WebSocket pushes the
event as it lands; for signal-driven strategies where the first seconds decide
the fill, that is the only thing that makes sense.

- Social alerts for trading bots: https://1322.io/use-cases/trading-bot-social-alerts
- The real-time API: https://1322.io/monitoring-api
- Event schema / docs: https://1322.io/docs

## Event shape

```json
{ "platform": "x", "handle": "examplekol", "content": "...", "coinPairs": ["BTCUSDT"], "timestamp": "2026-06-17T12:00:00Z" }
```

Normalized across every platform. `coinPairs` is parsed for Binance Square.

## Run

```bash
pip install websockets
API_KEY=your-key WS_URL=wss://1322.io/your-ws-path python main.py
```

Replace the `on_signal()` body with your strategy: match tickers / contract
addresses, route by author, fan out to multiple strategies, or place an order.

Get an API key + WebSocket path from the dashboard (from $250/mo):
https://1322.io/pricing

## Related

- Prediction-market signal router: https://github.com/1322monitors/prediction-market-router
- KOL tweet alert bot: https://github.com/1322monitors/kol-tweet-alert-bot
- Async Python client for the 1322 API: https://github.com/1322monitors/1322-python
- Binance Square: https://github.com/1322monitors/binance-square-realtime
- All seven platforms: https://github.com/1322monitors/social-monitor-examples

MIT licensed.
