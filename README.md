# Scam-message checker

A browser prototype built for the CodeExp2026 hackathon. Paste a suspicious message to inspect common manipulation signals and get a reply template that gives you time to verify the sender.

The detector is a small, inspectable set of weighted rules. A Singapore map, sample reports, simulated chat, and an incoming-call animation show how that check could sit within a broader scam-awareness interface.

[How the check works](#how-the-check-works) · [Run locally](#run-locally) · [Project structure](#project-structure)

## How the check works

The browser matches six signal groups with regular expressions: urgency, suspicious links, credential requests, rewards, threats, and payment requests. It adds the matched weights, applies length and punctuation adjustments, and caps the score at `99`.

Scores below `40` receive a Low label. Scores of `40` or more receive Medium, and scores of `75` or more receive High. The label selects a reply template. The interface lists the matched signals so you can inspect what triggered the score.

The displayed percentage is a heuristic score, not a measured probability. A low score does not verify a sender, a request, or the contents of a linked website.

## Stack and design

| Choice | Role in this prototype |
| --- | --- |
| HTML and CSS | Define the dashboard, map, message form, and call simulation without a frontend framework. |
| JavaScript ES modules | Separate the pure scoring and reply functions from DOM interactions and sample data. |
| Regular expressions | Make each signal and its weight visible in [src/scamDetector.mjs](src/scamDetector.mjs). No model call is required. |
| Node.js and Python's HTTP server | Run dependency-free detector checks and serve the local page. |

Message analysis runs in the browser. The application has no backend, live incident feed, telephone integration, or AI calling service. Report amounts, map markers, points, and stalled minutes are demonstration data.

## Run locally

Install Node.js with npm and Python 3. No package installation is required.

```sh
git clone https://github.com/Neonat/scam-message-checker.git
cd scam-message-checker
npm run dev
```

Open [localhost:5173](http://localhost:5173). Paste a message or cycle through the samples. **Send stall reply** adds a simulated exchange to the page. The call control animates a local demonstration and does not contact anyone.

## Project structure

| Location | Responsibility |
| --- | --- |
| [src/scamDetector.mjs](src/scamDetector.mjs) | Signal weights, score thresholds, and reply templates |
| [src/app.mjs](src/app.mjs) | DOM updates, report data, sample messages, and simulations |
| [index.html](index.html) and [styles.css](styles.css) | Page layout and styling |
| [assets/](assets/) | Background and Singapore map images |
| [tests/scamDetector.test.mjs](tests/scamDetector.test.mjs) | Deterministic detector assertions |

## Checks and changes

```sh
npm test
```

The tests cover high- and low-risk examples and the high-risk reply template. They do not measure false positives, false negatives, or real-world detection accuracy.

When changing a signal or its weight, add message examples that show the intended score and any benign wording affected by the rule. Keep simulated reports distinguishable from real incident data.

## License

No project license is included. The repository does not document separate licensing for the bundled images.
