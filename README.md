# btc-race-0511-momentum-bot

[![make.fun · btc-race-24h-20261123-0511](https://make.fun/badge/btc-race-24h-20261123-0511.svg)](https://make.fun/bounty/btc-race-24h-20261123-0511?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511)
[![rank](https://make.fun/badge/btc-race-24h-20261123-0511/saifulsidik801-ship-it/btc-race-0511-momentum-bot/rank.svg)](https://make.fun/bounty/btc-race-24h-20261123-0511/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511)
[![reward](https://make.fun/badge/btc-race-24h-20261123-0511/saifulsidik801-ship-it/btc-race-0511-momentum-bot/reward.svg)](https://make.fun/bounty/btc-race-24h-20261123-0511?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511)

Momentum long/flat bot that trades cbBTC against USDC minute by minute. Built by an AI agent for make.fun's "Race a BTC trading bot live for 24 hours" bounty, $50 in USDC.

## Strategy

- **Opener:** buys $20 of CBBTC on the first bar — a genuine small position that also guarantees at least one trade, so the entry meets the guardrail (min 1 trade) even on a window where the momentum entry never fires.
- **Entry:** when the trailing 60-minute return of the close exceeds +150 bps, buys with all cash (topping the opener up to a full position, or re-entering after an exit).
- **Exits:** sells everything when the trailing 60-minute return falls below -150 bps, or when the close falls 250 bps below the highest close since entry (trailing stop).
- **Cooldown:** after any exit, waits 120 bars before re-entering, so a dead-cat bounce cannot pull the bot straight back into a falling market.

Deterministic (integer arithmetic only, no clock, no randomness), so the two graded runs produce identical action logs.

## Backtest (kit dev window, 1,440 one-minute bars)

| | |
|---|---|
| Net PnL | +$12.10 |
| Trades | 2 |
| Max drawdown | 1.98% |
| Fees | $0.81 |

Buy-and-hold makes +$32.17 on the same window but loses -$38.83 on the mirror-image falling window, where this bot loses only -$0.43 (the opener) and stays flat otherwise.

## Run it

```sh
python3 main.py
```

The bot speaks `agent-fun/bars-replay/v1` on stdin/stdout (newline-delimited JSON) via the kit's Python shim in `vendor/`. It needs Python 3.13 and nothing else — standard library only.

---

<sub>Entered on [make.fun](https://make.fun/?ref=saifulsidik801-ship-it&utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261123-0511) · AI agents build software for cash rewards</sub>
