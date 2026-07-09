# What a Morpho integration looks like

Reference flows for teams integrating Morpho. Each demo runs the full lifecycle —
discover a market or vault, configure a position, execute, then manage it — and exposes
the SDK / contract calls behind every step in a collapsible **Blueprint** panel.

Nothing touches a chain. All numbers are simulated.

## The four demos

| Demo | Protocol | What it covers |
|---|---|---|
| **Earn** | Morpho Vaults | Deposit, withdraw, rewards, vault liquidity limits |
| **Variable-rate borrow** | Morpho Blue | Supply collateral, borrow, repay, add collateral, LTV & liquidation |
| **Fixed-rate borrow** | Morpho Midnight | Fixed APY to a maturity date, repay at par, maturity countdown |
| **Edge case sandbox** | All | Six positions across all products, three already in states an integration must handle |

The sandbox seeds a vault short on liquidity, a variable loan at high LTV, and a fixed
loan three days from maturity — each next to a healthy sibling. Clicking any row opens
that product's detail view.

## Contents

    index.html     the entire app — no build step, no dependencies
    vercel.json    static config + basic security headers

## Run locally

Open `index.html` in a browser. That's it.

Or serve it:

    npx serve .

## Deploy to Vercel

From this directory:

    npx vercel            # preview deployment
    npx vercel --prod     # production

Vercel auto-detects it as a static site. No framework preset, no build command,
output directory is the project root.

Alternatively, drag this folder onto https://vercel.com/new — it will deploy as-is.

## Known placeholders

Three things to replace before this goes anywhere public:

- The legal footer references **`XXX's Terms of Use`**.
- The Morpho butterfly mark (top-bar logo and the "Powered by Morpho" badge) is a
  hand-traced SVG, not the official brand asset. Swap `MORPHO_MARK` in `index.html`.
- Token logos load from the Trust Wallet CDN, with an inline SVG for cbBTC and a
  coloured-initials fallback, so the UI degrades cleanly if the CDN is blocked.

## Conventions worth keeping

- **Colour means risk, and only risk.** Amber for constraints (low liquidity), red for
  proximity to liquidation. Rates are never colour-coded.
- **Recap rows follow one order:** outcome → rate → cost → obligation → risk.
- **Approvals and multi-step sequences are bundled** into a single signature wherever
  the protocol allows it. The permit is encoded but never surfaced in the UI.
- **Protocol vocabulary lives in the Blueprint panels**, not the user-facing copy.
