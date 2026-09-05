# Open Hedgie

**Hedgie is a private household receipt log and spending report.**

No account. No subscription. No company holding your data. Just a single file you open in a browser — on any device, any time, fully offline if you want it to be.

The current interface is intentionally compact: record income and purchases, track total and monthly savings, review monthly or yearly reports, and keep the app available offline. Existing local data and compatible sync payloads remain readable.

**Stable:** [hedgie.pages.dev](https://hedgie.pages.dev) — Cloudflare Pages, fully tested releases<br>
**Pilot:** [lancebramsay.github.io/hedgie](https://lancebramsay.github.io/hedgie) — GitHub Pages, latest updates<br>
**Current stable:** v2.5.9 | **Pilot:** v2.5.9

---

## Current features

### Receipt logging
- Record category, amount, vendor, note, date, and recurring schedule
- Vendor memory with suggestions and automatic pruning
- Edit and delete receipts, filter by category, and review a selected month
- Existing recurring bills continue to auto-log when their saved data is present

### Income and savings
- Record income by source, amount, date, note, and optional recurring schedule
- Edit and delete income records; stopping a recurring income keeps existing entries
- Savings overview shows cumulative income, cumulative spending, and total savings across all history
- Set a monthly savings target and track actual savings with a bounded progress bar
- Core data is saved immediately in the browser's local storage and restored on reload

### Reports
- Monthly income, actual spending, monthly savings, and monthly savings target progress
- Spending breakdown by category with progress indicators
- Yearly income is calculated from actual income records
- Yearly spending overview (Hibernation View), including archived receipts

### Local data and compatibility
- Core receipt and report data stays in the browser and works offline
- Existing sync payloads support GitHub Gist, Dropbox, JSONBin.io, and self-hosted endpoints
- HMAC-SHA256 signed payloads with a shared secret key
- Optional AES-256-GCM payload encryption (derived from shared key via PBKDF2)
- Conflict resolution modal and automatic receipt merging
- Auto-archive moves receipts older than the prior calendar year to a read-only archive; configurable retention window (1–10 years, or keep forever)

The current interface does not expose the old provider-configuration, backup, or settings panels. Previously saved credentials and compatible payload fields are retained for migration and sync compatibility.

### Den (Preview)

Den is hidden by default. If an existing local profile has the Den preview enabled, the tab remains available for tracking long-term assets and liabilities. Den data remains part of the shared sync payload.

- **Net worth metrics** — net worth, total assets, total debt, portfolio G/L at the top of the tab
- **Net Worth chart** — donut pie chart showing equity, stocks, ETFs, crypto, CD/savings, and savings goals
- **Portfolio Mix chart** — composition of the investment portfolio
- **Liabilities** — loans, credit, leases, and other financing accounts with balance, interest rate, term, and payoff estimate; optional asset value field for equity-building debts
- **Portfolio** — stocks, ETFs, crypto, CD/Savings, and other positions; CD/Savings entries calculate compound interest from principal, APY, and deposit date; purchase receipts can be linked to auto-track cost basis and units
- **Performance chart** — aggregate portfolio value over 1D / 1W / 1M / 3M / 6M / 1Y; all ranges are purchase-date-aware
- **Savings goals** — named targets with progress bar
- **Live price feed** — CoinGecko (free, no key), Finnhub, Twelve Data, Alpha Vantage
- **Wallet balances** — connect a public 0x address or MetaMask/Brave/Coinbase Wallet; pulls ETH, POL, USDC, USDT, and DAI across Ethereum, Arbitrum, Base, and Polygon
- **Transaction import** — Etherscan API key optional; fetches transaction history across all enabled chains into a review queue before logging as receipts; auto-import mode available

### App and device
- Dark mode — toggle from the tab bar
- Installable PWA: 📲 button on Android/desktop; Share → Add to Home Screen on iOS/iPadOS
- Swipe left/right between tabs on any touch screen
- Multi-user receipt attribution — existing display names are retained in saved receipts

---

## Getting started

1. Download `index.html` from the [releases page](https://github.com/lancebramsay/hedgie/releases) or open the [hosted version](https://hedgie.pages.dev)
2. Open in Chrome, Safari, Firefox, or Brave
3. Log purchases in **Log a purchase** as you spend
4. Log paychecks and other money received in **Log income**
5. Set the current month's target in **Monthly savings target**
6. Review **Monthly report** for income, spending, savings, and yearly totals

Works fully offline. No internet required for core features.

---

## Sync compatibility

The current interface has no provider setup panel. Existing `hedgie_settings` values are still loaded, so profiles configured by an earlier compatible version can continue to use their saved provider and credentials.

### Self-hosted endpoint

Expects GET (returns JSON) and PUT (stores JSON) on one URL. Optional Bearer token auth.

```bash
npm install express
HEDGIE_TOKEN=secret node server.js
```

---

## Security and compatibility

- Shared secret keys, provider credentials, and encryption preferences from compatible saved profiles remain local to the browser
- HMAC-SHA256 payload signing — sync rejected on key mismatch
- Optional AES-256-GCM payload encryption — requires HTTPS
- Key derivation: `PBKDF2(sharedSecret, salt='hedgie-aes-v1', 100,000 iterations) → AES-256 key`
- API keys (price feeds, Etherscan) are stored only in `localStorage` on-device and are never included in sync payloads

---

## Sync safety

- **Empty session → always pulls.** A blank session cannot push to the cloud, even if preferences like dark mode were changed.
- **First sync with local data → user confirms.** Hedgie fetches the cloud version and shows a pull-or-push dialog before touching anything.
- **Conflict resolution.** If compatible saved budget data differs between users, a modal lets you choose which plan to keep. Receipts are always merged automatically.

---

## PWA install

### Android / Desktop
The 📲 button appears in the tab bar when the browser offers installation. Tap to install.

### iOS / iPadOS
A banner appears with instructions: tap **Share ⬆** in the browser toolbar → **Add to Home Screen**.

Once installed as a PWA, the button and banner hide automatically.

---

## Limits

| Resource | Warning at | Hard limit |
|---|---|---|
| Vendor memory | 160 | 200 (auto-prunes oldest) |

---

## Compatibility

| Browser | Support |
|---|---|
| Chrome (desktop + Android) | ✓ Full |
| Safari (macOS + iOS) | ✓ Full |
| Brave | ✓ Full |
| Firefox | ✓ Full (no PWA install prompt) |

> Encryption and HMAC signing require HTTPS or localhost. `file://` URLs skip signing.

---

## Deployment

| Channel | URL | Source | Purpose |
|---|---|---|---|
| **Stable** | [hedgie.pages.dev](https://hedgie.pages.dev) | Cloudflare Pages — `stable` branch | Fully tested, recommended for everyday use |
| **Pilot** | [lancebramsay.github.io/hedgie](https://lancebramsay.github.io/hedgie) | GitHub Pages — `main` branch | Latest updates, may include changes still being validated |

---

## Roadmap

### Phase 1 — Now: Open Hedgie

The free, open-source web edition. The current release focuses on receipt logging and monthly/yearly reports, with compatible Den data and features retained for existing profiles.

### Phase 2 — Next: NFT ecosystem

The **Hedgehog Den** NFT collection unlocks full Den features on Open Hedgie — no account, no subscription. Each NFT is a unique generative hedgehog and a self-sovereign Den license, valid across Ethereum, Arbitrum, Base, and Polygon.

A separate **Community App** serves as the ecosystem hub: NFT marketplace, staking hub (earn `$HEDGE` tokens), and a non-binding community signal board.

### Phase 3 — Later: Native Hedgie (iOS / macOS)

A native SwiftUI app with CloudKit sync, Sign in with Apple, and iCloud Keychain wallet backup. Den features included in the paid App Store download.

---

## Contributing

PRs and issues welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

MIT — see [LICENSE](LICENSE).
