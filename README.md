# MindSparkd website

The landing page for mindsparkd.com, plus the public pages the app stores and
Meta require: privacy policy, terms, support, and data deletion. Plain static
HTML — no build step, no framework, nothing to install.

## The pages

| File | What it is for |
|------|----------------|
| `index.html` | Landing page |
| `privacy.html` | **Required by Apple** (App Store Connect) and by Meta |
| `terms.html` | Required by Apple once subscriptions exist; the EULA |
| `support.html` | **Required by Apple** — the support URL in App Store Connect |
| `delete-data.html` | **Required by Meta** to take the app out of Development mode |
| `404.html` | Served by Cloudflare Pages for any unknown path; its links are root-relative for that reason |
| `assets/style.css` | Shared by every page: palette (from the app's `src/lib/theme.ts`), header, footer, the legal pages' layout |
| `assets/home.css` | The landing page only, including the CSS phone mockups |
| `assets/bg/` | Background photos from the app's own catalogue (Pexels), resized for the web |

The landing page merges the three directions on the website canvas
(2026-09-27): the night-sky hero and the strip of backgrounds from B; the
quote wall and feature grid from C; the genre chips and privacy card from A.
The quote wall's headline, "Less fridge magnet. More *that's so me.*", is new.

The phones are drawn in CSS, not screenshots. Every size inside one is in `em`
and the frame's font-size is its width divided by 29, so setting `--pw` alone
scales a whole phone. Swap in real screenshots when the App Store ones exist.

## Editing

Open the file and edit it. That is the whole workflow — the pages are plain
HTML and each one carries its own header and footer, so there is nothing to
rebuild and nothing to regenerate.

To see a change before pushing, open the file in a browser.

If you change the header or footer, change it in all six pages. That is the
trade for having no build step, and these pages change rarely.

## Publishing

**Cloudflare Pages** serves the site at `https://mindsparkd.com`, deploying
`main` on every push: framework preset *None*, no build command, output
directory `/`. Branches and pull requests get their own preview URL. Cloudflare
strips `.html`, so `privacy.html` is served at `/privacy`.

**GitHub Pages** still serves the same `main` at
`https://raffyg23.github.io/mind-sparkd-website/`. Keep it on until every
saved URL has moved to mindsparkd.com: Google Auth Platform branding, the Meta
app settings, App Store Connect, and the Terms / Privacy links in the app's
sign-in screen.

## Keeping it honest

`privacy.html` and `delete-data.html` describe what the app actually does. If
the app starts collecting something new — analytics, ads, a new sign-in
provider, a new kind of upload — these pages have to change with it, in the
same release. A privacy policy that no longer matches the app is worse than
not having one.

Claims that depend on code or services elsewhere:

- **"There are no analytics or tracking"** (privacy page). True as long as no
  analytics SDK is added to the mobile app. Ads and analytics are planned, so
  the landing page deliberately does not make this claim.
- **"Deleting your account deletes your uploaded photos."** True as long as
  `delete_auth_user` in the API sweeps the `backgrounds` and `avatars` storage
  buckets. Database rows cascade on their own; storage objects do not.
- **"25+ genres", "60+ backgrounds", "thousands of quotes"** (landing page).
  Rounded on purpose so a new genre needs no edit; change them only if the
  library or the background catalogue shrinks below them.
- **"Coming soon to the App Store".** When the app is live, make the badge a
  link to `https://apps.apple.com/app/id6801309940` (there is a comment on it).
- **hello@mindsparkd.com** is the contact on every page. It works because
  Cloudflare Email Routing forwards it to the MindSparkd Gmail; that route has
  to stay up.
