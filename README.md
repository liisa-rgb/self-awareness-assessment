# Self-awareness self-assessment — Nordic Edge

Static page with eleven slider questions. The respondent saves their snapshot
as a PDF using the browser's print menu — a print stylesheet renders the
sliders, positions, and chosen values cleanly.

## Stack

- Single static `index.html` (no build step)
- Brand assets under `assets/` — pulled from the Nordic Edge design system
- No JS dependencies, no client-side libraries

## Local preview

Open `index.html` in a browser, or serve the folder:

```sh
python3 -m http.server 8765
# then visit http://localhost:8765/
```

To verify the print output: hit `⌘P` (Mac) or `Ctrl+P` (Windows) — you should
see the title, then 11 questions each with a dark-blue track + marker at the
chosen position and a "Selected: X.X / 5" line.

## Deploy to Vercel

Push to a GitHub repo, then in Vercel:

1. **Add New → Project → Import Git Repository.**
2. Select the repo. Vercel auto-detects it as a static site.
3. Click **Deploy**. You'll get a URL like
   `self-awareness-assessment.vercel.app`.
4. (Optional) **Settings → Domains** to add e.g.
   `assessment.nordicedge.fi`.

No build command, output directory, or `vercel.json` is needed.

## Roadmap

- **ActiveCampaign integration.** Add a small Vercel serverless function that
  posts the email + a tag (`took-self-awareness-assessment`) to AC, so the
  assessment becomes a tracked lead-magnet entry. Tool currently does not
  collect any data.

## Fonts and brand assets

`assets/colors_and_type.css` is the canonical Nordic Edge token file. The
fonts (Söhne Breit, Anton, Geist Bold/Black) are stored under
`assets/fonts/`. Logos under `assets/logos/`.

If the design system changes, replace `assets/colors_and_type.css` and the
font/logo files; nothing in `index.html` depends on the file contents beyond
the CSS variables.
