# code_exp — scam-message checker

A browser prototype for spotting scam-message signals and suggesting replies that buy time to verify a request. Message analysis uses weighted regular-expression rules for urgency, suspicious links, credential requests, reward bait, threats and payment requests.

The displayed score is a heuristic, rather than a measured probability. Map reports, loss figures, chat exchanges, calls and points are sample data or local simulations. Analysis runs in the browser; the prototype has no backend service.

## Run locally

You need Node.js/npm for the scripts and tests, Python 3 for the development server, and a modern browser. There are no package dependencies to install.

```sh
git clone https://github.com/Neonat/code_exp.git
cd code_exp
npm run dev
```

Open [localhost:5173](http://localhost:5173). Paste a message or cycle through the samples to see the matched signals and suggested stall reply.

## Check

```sh
npm test
```

The existing deterministic tests cover high- and low-risk examples and the high-risk reply template.

## Source

- `src/scamDetector.mjs` — scoring rules and reply templates.
- `src/app.mjs` — interface behavior and sample reports.
- `index.html`, `styles.css`, `assets/` — page, styling and images.
- `tests/scamDetector.test.mjs` — Node.js assertions for the detector.
