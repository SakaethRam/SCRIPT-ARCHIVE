# WORKFLOW

A single, self-contained HTML page: `index.html`, titled "ORBIT | Workflow Demonstration." No build step, no external app shell; open it directly in a browser.

## What it is

A standalone visual demonstration page, styled in the same dark background / olive accent palette (`--olive: #667344`, `--olive-light: #a3b07a`) used elsewhere across this author's material, using Space Grotesk and DM Mono for display and monospace text respectively, loaded from Google Fonts.

## Structure

Everything (HTML, CSS, and presumably JS further down the file) lives in this one file rather than being split into separate assets. That's a reasonable choice for a single demonstration page meant to be shared or opened standalone, but it does mean any edit touches one large file rather than a smaller, scoped one; if this page grows into something with more interactive behavior, splitting the `<style>` block and any script into separate `.css`/`.js` files would make it easier to maintain.

## Running it

No server or build tooling needed:

```bash
open WORKFLOW/index.html        # macOS
start WORKFLOW\index.html       # Windows
xdg-open WORKFLOW/index.html    # Linux
```

Or open it directly in a browser via File → Open.

## If this needs to be shared beyond a local file

Since it's a single static HTML file with no server-side dependency, it's a direct fit for static hosting (Netlify, GitHub Pages, Vercel) with zero configuration: drop the file in, no build command required. Worth doing if "ORBIT" is meant to be shown to someone else rather than opened locally each time.
