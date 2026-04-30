# Self-awareness self-assessment — Nordic Edge

Static page that asks eleven slider questions, generates a PDF snapshot of the
respondent's answers, and emails it to the address they enter.

## Stack

- Single static `index.html` (no build step)
- Brand assets under `assets/` — pulled from the Nordic Edge design system
- `jsPDF` (CDN) for client-side PDF generation
- `EmailJS` (CDN) for delivering the PDF to the respondent's inbox

## Local preview

Open `index.html` in a browser. The form works fully without setup; if EmailJS
isn't configured, respondents are offered a direct download instead of an email.

## Email delivery setup (one-time, ~3 min)

1. Sign up at https://www.emailjs.com (free tier: 200 sends/month).
2. **Email Services → Add New Service.** Connect Gmail or any provider. Note
   the **service ID**.
3. **Email Templates → Create New Template.** Use these fields:
   - **To Email:** `{{to_email}}`
   - **From Name:** Nordic Edge
   - **Subject:** Your self-awareness assessment result
   - **Content:** any text you like — example below.
   - **Attachments:** enable. Filename `self-awareness-result.pdf`, content
     from variable `content`, encoding `base64`.

   Example body:
   ```
   Hi,

   Thanks for taking the self-awareness self-assessment.
   Your snapshot is attached as a PDF.

   — Nordic Edge
   nordicedge.fi
   ```

4. **Account → General.** Copy your **public key**.
5. Paste the three values into the `CONFIG` block near the top of the
   `<script>` in `index.html`:
   ```js
   const EMAILJS_PUBLIC_KEY  = "kV1aBcDeFgHiJk";
   const EMAILJS_SERVICE_ID  = "service_abc123";
   const EMAILJS_TEMPLATE_ID = "template_xyz789";
   ```
6. Commit and redeploy.

## Deploy to Vercel

Push this folder to a GitHub repo, then in Vercel:

1. **Add New → Project → Import Git Repository.**
2. Select the repo. Vercel auto-detects it as a static site.
3. Click **Deploy**. You'll get a URL like
   `self-awareness-assessment.vercel.app`.
4. (Optional) **Settings → Domains** to add e.g.
   `assessment.nordicedge.fi`.

No build command, output directory, or `vercel.json` is needed.

## Fonts and brand assets

`assets/colors_and_type.css` is the canonical Nordic Edge token file. The
fonts (Söhne Breit, Anton, Geist Bold/Black) are stored under
`assets/fonts/`. Logos under `assets/logos/`.

If the design system changes, replace `assets/colors_and_type.css` and the
font/logo files; nothing in `index.html` depends on the file contents beyond
the CSS variables.

## What's NOT in here

- No analytics. Add Plausible / Fathom / GA in the `<head>` if needed.
- No storage of submissions on your side — the PDF goes only to the
  respondent. If you want a copy too, change the EmailJS template to also
  send to your address (or add a `cc_email` variable to the template).
- No Finnish version yet. If you want one, duplicate the page or wire up a
  language switch.
