# The public site, and why it exists

Three static pages: a home page, a privacy policy and terms. They exist because Google will not let an
**External** OAuth app leave *Testing* without a home page, a privacy policy URL and a matching authorized
domain - a console behaviour since about August 2026 that catches personal, single-user apps like this one.
Staying in Testing was the alternative, and it expires the refresh token every 7 days.

Nothing here is decorative: the privacy policy is the one Google's reviewers and the consent screen point
at, so it says exactly what the uploader touches and nothing it does not.

## Done (2026-11-21)

- Public repository **`hesamhakim/hesamhakim.github.io`** created.
- These pages pushed to it. Commits use `hesamhakim@users.noreply.github.com` rather than your real
  address, since a public repository's commit metadata is readable by anyone; GitHub still attributes them
  to your account.
- GitHub Pages enabled on `main` / root, built, and serving:
  - <https://hesamhakim.github.io/>
  - <https://hesamhakim.github.io/privacy.html>
  - <https://hesamhakim.github.io/terms.html>

This folder is its own git repository, separate from the research one - the site is public and the
research repo is not. `site/.git` is ignored by the outer repository.

## Your turn - the parts that need your Google account

**1. Verify the domain in Search Console.** Go to <https://search.google.com/search-console>, signed in as
the account that owns the Cloud project. Add a property of type **URL prefix**: `https://hesamhakim.github.io/`.
Choose either method and hand me the result - I can push it in seconds:

- **HTML file**: it offers a file like `google1a2b3c4d5e.html`. Tell me its name and contents and I will
  commit it to the site; then click Verify.
- **HTML tag**: it gives a `<meta name="google-site-verification" content="...">`. Paste it to me and I
  will put it in `index.html`'s `<head>`; then click Verify.

**2. Fill the Branding page** (Google Auth Platform → Branding):

| Field | Value |
|---|---|
| Application home page | `https://hesamhakim.github.io/` |
| Application privacy policy link | `https://hesamhakim.github.io/privacy.html` |
| Application terms of service link | `https://hesamhakim.github.io/terms.html` |
| Authorized domains → Add domain | `hesamhakim.github.io` |

Leave the **App logo** empty - uploading one forces the app into verification, which is not otherwise
needed. Save.

**3. Audience → Publish app.** The button should now be active. Afterwards the consent screen shows
"Google hasn't verified this app"; **Advanced → Go to … (unsafe)** is the expected path for your own app,
and refresh tokens stop expiring after seven days.

**4. Run the login** (the Mac acts only as a browser; the token lands on the HPC):

```bash
pip install google-auth-oauthlib
cd /scratch/g/he301766/projects/PhenoMotion_visualization_ecosystem_for_biology/phenomotion
python tools/youtube_login_browser.py ~/Downloads/client_secret_desktop.json
```

Then on the HPC, `mv phenomotion/tools/youtube_token.json ~/.config/phenomotion/youtube_token.json`.

## One thing you may want to change

`privacy.html` ends by pointing at the consent screen's contact address rather than printing an email on a
public page, where it would be scraped. If you would rather show one, say so and I will add it - there is
an HTML comment marking the spot.

## Changing the pages later

```bash
cd /scratch/g/he301766/projects/PhenoMotion_visualization_ecosystem_for_biology/site
# edit, then
git add -A && git commit -m "..." && git push
```

Pages rebuilds within a minute or so.
