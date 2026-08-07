# Learn — personal reference library

A static homepage for `github.io` that lists your reference materials, plus a
tool to add new ones without hand-editing JSON every time.

## Files

```
index.html       ← the homepage (reads manifest.json, renders cards)
manage.html       ← the "+ Add material" upload tool
manifest.json     ← the list of materials shown on the homepage
assets/           ← your material files live here (e.g. algorithm-atlas.html)
```

## Set it up on GitHub Pages

1. Create (or reuse) a repo — if it's named `yourname.github.io`, Pages serves
   it at the root automatically. Otherwise enable Pages in the repo's
   **Settings → Pages** and pick the branch to publish.
2. Put these four items (`index.html`, `manage.html`, `manifest.json`,
   `assets/`) at the root of that repo.
3. Push. Your homepage is live at `https://yourname.github.io/` (or
   `.../reponame/` if it's not the special `username.github.io` repo).

## Adding a new material — two ways

**Manual (no setup, always works):**
Open `manage.html` → `+ Add material`, fill in the file and details, and
click **Download HTML file**. It also gives you the exact JSON snippet to
paste into `manifest.json`. Save the downloaded file into `/assets`, paste
the snippet into the manifest's array, then commit + push (or use GitHub's
web UI: repo → folder → **Add file → Upload files**).

**Connected (one click, needs a token once):**
On `manage.html`, check **"Connect to GitHub for one-click publish"** and
fill in:
- your GitHub username
- the repo name
- the branch (usually `main`)
- a **fine-grained Personal Access Token** with *only* `Contents: Read and
  write` permission, scoped to that one repo
  ([create one here](https://github.com/settings/personal-access-tokens/new))

Click **Save connection**, then **Publish to GitHub** — it commits the file
and updates `manifest.json` for you via GitHub's API, straight from the
browser. No server involved.

The token is stored only in that browser's local storage. Don't leave it
saved on a shared or public computer, and revoke it from GitHub's settings
any time you want to cut off access.

## Notes

- `index.html` fetches `manifest.json` with `fetch()`, which browsers block
  under the `file://` protocol. To preview locally, run a tiny server from
  this folder, e.g. `python3 -m http.server`, then open
  `http://localhost:8000`. It works normally once published to GitHub Pages.
- Categories on the homepage are derived automatically from whatever you put
  in each entry's `category` field — no need to register them anywhere.
