# The public site, and why it exists

Three static pages: a home page, a privacy policy and terms. They exist because Google will not let an
**External** OAuth app leave *Testing* without a home page, a privacy policy URL and a matching authorized
domain - a console behaviour since about August 2026 that catches personal, single-user apps like this one.
Staying in Testing was the alternative, and it expires the refresh token every 7 days.

Nothing here is decorative: the privacy policy is the one Google's reviewers and the consent screen point
at, so it says exactly what the uploader touches and nothing it does not.

## Putting it up (about 15 minutes, once)

1. **Create a public repository named `hesamhakim.github.io`** on GitHub. The name must match the account
   exactly; that is what makes it a user site served at the root.

2. **Push these three files to it:**

   ```bash
   cd /scratch/g/he301766/projects/PhenoMotion_visualization_ecosystem_for_biology/site
   git init -b main
   git add index.html privacy.html terms.html
   git commit -m "PhenoMotion: home page, privacy policy, terms"
   git remote add origin git@github.com:hesamhakim/hesamhakim.github.io.git
   git push -u origin main
   ```

   (`git init` here makes a *second*, independent repository inside this folder. That is deliberate - this
   site is public and the research repository is not. The outer repository ignores `site/.git`.)

3. **Turn on Pages**: repository → Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`.
   Give it a minute, then check <https://hesamhakim.github.io/> loads.

4. **Verify the domain** at <https://search.google.com/search-console>. Add a property of type **URL
   prefix** for `https://hesamhakim.github.io/`, choose the **HTML file** method, download the
   `google*.html` file it gives you, commit it to the same repository, push, then click Verify. It must be
   the Google account that owns the Cloud project.

5. **Fill the Branding page** in Google Auth Platform:

   | Field | Value |
   |---|---|
   | Application home page | `https://hesamhakim.github.io/` |
   | Application privacy policy link | `https://hesamhakim.github.io/privacy.html` |
   | Application terms of service link | `https://hesamhakim.github.io/terms.html` |
   | Authorized domains → Add domain | `hesamhakim.github.io` |

   Leave the **App logo** empty - uploading one forces the app into verification, which is not otherwise
   needed. Save.

6. **Audience → Publish app.** The button should now be active. Afterwards the consent screen shows
   "Google hasn't verified this app"; **Advanced → Go to … (unsafe)** is the expected path for your own
   app, and refresh tokens stop expiring after seven days.

## One thing to edit first

`privacy.html` ends with a contact line that points at the consent screen rather than printing an email
address, so that publishing this page does not put your address on the open web for scrapers. If you would
rather show one, replace that sentence - there is an HTML comment marking the spot.
