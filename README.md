# Scam-message checker

A browser prototype built for the **Code EXP 2026 hackathon** to help people inspect suspicious messages and pause before acting on a request. It highlights common manipulation signals and suggests a reply that buys time to verify the sender.

## What is built

- Paste a message or choose a sample to see a heuristic risk score and matched signals.
- Weighted regular-expression rules check urgency, suspicious links, credential requests, reward bait, threats and payment requests.
- A reply template changes with the detected risk level.
- A Singapore map, report list, chat exchange, incoming-call sequence and points display demonstrate the surrounding interface using sample data and local simulations.

All analysis runs in the browser using JavaScript. There is no backend, live incident feed, telephone integration or AI calling service. The displayed score is a rule-based indicator, not a measured probability that a message is a scam.

## Try it locally

You need Node.js/npm for the scripts and checks, Python 3 for the development server, and a modern browser. There are no package dependencies to install.

```sh
git clone https://github.com/Neonat/scam-message-checker.git
cd scam-message-checker
npm run dev
```

Open [localhost:5173](http://localhost:5173), then paste a message or cycle through the examples. The prototype does not verify a sender's identity or the contents of linked websites; a low score does not establish that a message is safe.

## Existing checks

```sh
npm test
```

The deterministic Node.js assertions cover high- and low-risk examples and the high-risk reply template. They do not establish real-world detection accuracy.

## Source guide

| Location | Purpose |
| --- | --- |
| [`src/scamDetector.mjs`](src/scamDetector.mjs) | Scoring rules and reply templates. |
| [`src/app.mjs`](src/app.mjs) | Interface behaviour, sample reports and simulations. |
| [`index.html`](index.html), [`styles.css`](styles.css), [`assets/`](assets/) | Page structure, styling and images. |
| [`tests/scamDetector.test.mjs`](tests/scamDetector.test.mjs) | Existing detector assertions. |
