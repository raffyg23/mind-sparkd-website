# MindSparkd website

The public pages the app stores and Meta require: privacy policy, terms,
support, and data deletion. Plain static HTML — no build step, no framework,
nothing to install.

## The pages

| File | What it is for |
|------|----------------|
| `index.html` | Landing page |
| `privacy.html` | **Required by Apple** (App Store Connect) and by Meta |
| `terms.html` | Required by Apple once subscriptions exist; the EULA |
| `support.html` | **Required by Apple** — the support URL in App Store Connect |
| `delete-data.html` | **Required by Meta** to take the app out of Development mode |
| `assets/style.css` | All the styling. The palette matches the app's `src/lib/theme.ts` |

## Editing

Open the file and edit it. That is the whole workflow — the pages are plain
HTML and each one carries its own header and footer, so there is nothing to
rebuild and nothing to regenerate.

To see a change before pushing, open the file in a browser.

If you change the footer, it appears in all five pages; change it in each.
That is the trade for having no build step, and these pages change rarely.

## Publishing

The site is served by **GitHub Pages** from the `main` branch. Pushing to
`main` publishes it; give it a minute.

## Keeping it honest

`privacy.html` and `delete-data.html` describe what the app actually does. If
the app starts collecting something new — analytics, ads, a new sign-in
provider, a new kind of upload — these pages have to change with it, in the
same release. A privacy policy that no longer matches the app is worse than
not having one.

Two claims in particular are load-bearing, and both depend on code elsewhere:

- **"There are no analytics or tracking."** True as long as no analytics SDK
  is added to the mobile app.
- **"Deleting your account deletes your uploaded photos."** True as long as
  `delete_auth_user` in the API sweeps the `backgrounds` and `avatars` storage
  buckets. Database rows cascade on their own; storage objects do not.
