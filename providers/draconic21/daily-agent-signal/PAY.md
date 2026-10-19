---
name: daily-agent-signal
title: "draconic21 Daily Agent Signal"
description: "Daily Agent Signal: dated, ranked x402 market intelligence for agent commerce. One JSON brief per day with sha256-addressed revisions, a delta, and a dated archive; paid per call in USDC (Base or Solana) via x402."
use_case: "Use for x402 market intelligence, agent-commerce research, x402 seller and directory activity, and daily agent-economy briefs. Read the free /signal page and /signal/scorecard.json (misses included) before paying."
category: finance
service_url: https://draconic21-x402-api.onrender.com
openapi:
  path: openapi.json
---

Daily Agent Signal: dated, ranked x402 market intelligence for agent commerce, paid per call in USDC. Read the free [/signal](https://draconic21-x402-api.onrender.com/signal) page and [/signal/scorecard.json](https://draconic21-x402-api.onrender.com/signal/scorecard.json) (misses included) first. Sampled transfers and directory activity are not verified buyer revenue.

Each edition is a dated JSON brief. Its `sha256` is published free at `GET /health` (`signal.sha256`) and `GET /v1/signal_latest/example`, so an agent can tell whether a new edition exists before paying. Unpaid calls return HTTP 402 with an x402 v2 challenge offering USDC on Base (`eip155:8453`) and USDC on Solana mainnet (same amount).

## Free first

- `GET /signal`: headlines and SKU prices.
- `GET /signal/scorecard.json`: dated calls scored confirmed/partial/falsified/open, misses included.
- `GET /v1/signal_latest/example`: shape plus today's date and sha256 (no paid judgments).
- `GET /v1/signal_delta/availability`: which archive dates exist.

## Paid

| Price | Route |
|-------|-------|
| $0.03 | `POST`/`GET /v1/signal_latest` (today's edition) |
| $0.05 | `POST /v1/signal_delta` |
| $0.10 | `POST /v1/signal_history` |
| see `/signal` | `signal_continuity`, `signal_day`, `archive_tip_day`, `signal_topic_trace` |

## Spend-aware usage

- Check `GET /health` `signal.sha256` first; if it matches the edition you already hold, don't buy again.
- Pass `?expect_sha256=<sha256>` on `GET /v1/signal_latest` so you only pay for the revision you checked; a newer revision returns 409 before payment.
- Buy `signal_latest` once per edition; use `signal_delta` instead of re-buying history when you only need what changed.
