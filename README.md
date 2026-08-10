# Morning Brief

A personal markets dashboard for equity-derivatives-flavored morning prep: the tape, the vol complex, a week-ahead calendar, desk intel, an EQD learning toolkit, daily reads,  and a status panel for an autonomous, small-scale trading agent that runs each weekday morning.

**The site is encrypted at rest.** This repository and the published page contain only AES-256-encrypted content ([StatiCrypt](https://github.com/robinmoisson/staticrypt)); a password decrypts it in your browser. The password is never stored in this repo or on the host.

## How it works

One self-contained HTML file. Delayed market quotes refresh client-side (Cboe delayed indices, CoinGecko, ECB reference FX) whenever the page is open. Each weekday around 7:45 AM PT, a scheduled Claude agent reconciles the trading account and publishes a ~1 KB AES-256-encrypted data blob to a shared Drive folder. A GitHub Action here (8:20 AM PT) pulls the newest blob, decrypts it with a repo secret, splices it into the decrypted page shell, re-encrypts everything with StatiCrypt, and commits , GitHub Pages redeploys automatically. The plaintext dashboard never exists in this repo, in the Drive folder, or in any build log.

## Build

```bash
npx staticrypt dashboard.html -p "<password>" -d out --remember 30
```

The plaintext dashboard is never committed. `.staticrypt.json` holds only the non-secret salt (kept stable so "remember me" survives rebuilds).

## Disclaimer

Personal project. Nothing here is investment advice. Quotes are delayed and unofficial. Not affiliated with any employer, broker, or data vendor.
