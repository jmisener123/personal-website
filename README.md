# jessicamisener.com

Personal site for Jessica Misener — writer, editor, AI product builder.

Plain HTML and CSS. **No build step, no dependencies, no `npm install`.** Edit a
file, push, and Vercel deploys it. It will still work in ten years.

## Files

```
index.html            Home
about/                Bio, caption contest wins, photo
writing/              Landing: books + clips
writing/books/        Both books
writing/clips/        Journalism, with an outlet filter
work/                 AI & product work, talks
now/                  Running "what I'm up to" note
contact/              Email + LinkedIn + GitHub
404.html              Not-found page
assets/styles.css     All styling. Design tokens live at the top.
assets/favicon.svg
sitemap.xml           Static — add a <url> entry if you add a page
robots.txt
vercel.json           Redirects from the old Squarespace URLs, plus headers
```

## Editing

**Change colors or type:** the `:root` block at the top of `assets/styles.css`.
Every color, font, and size on the site comes from those variables, so changing
`--accent` there changes it everywhere.

**Add a clip:** open `writing/clips/index.html`, copy an existing `<li>` block,
paste it in date order (newest at top), and fill it in. Set `data-outlet` to the
publication name — the filter dropdown builds itself from those values, so
there's nothing else to update. The filter only appears once there are two or
more distinct outlets, and the list works fine with JavaScript off.

**Add a project:** copy a `<li class="card">` block in `work/index.html`.

**Add a page:** create `newpage/index.html` (a folder with an `index.html` gives
you the clean `/newpage/` URL), copy the header and footer from any existing
page, and add a `<url>` entry to `sitemap.xml`.

**Change the nav or footer:** these are duplicated across all nine HTML files —
the one real cost of skipping a build step. Search and replace across the repo.
On the current page, that page's nav link carries `aria-current="page"`.

## Search for these before launch

Placeholders are marked two ways:

- Tan callout boxes on the page (`class="todo"`) — visible in the browser.
  Search the repo for `class="todo"` and delete each block as you replace it.
- Text in `[square brackets]` — book titles, clip headlines, project details.

Also confirm: the email address (`hello@jessicamisener.com` appears in every
footer), the LinkedIn and GitHub URLs, and the copyright year.

Nothing was invented — no fake book titles, quotes, or publication details. The
example clips and projects are structural scaffolding with obvious blanks.

## Preview locally

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Any static server works.

Note that `python3 -m http.server` serves `/about` without the trailing-slash
redirect Vercel adds, and shows its own 404 page instead of `404.html`. Both
behave correctly once deployed.

## Deploying

Push to `main`. On Vercel: import the repo, framework preset **Other**, no build
command, output directory `.` (the repo root). `vercel.json` handles the
Squarespace redirects and security headers.

`/about` and `/contact` don't need explicit redirect rules — `trailingSlash: true`
sends them to `/about/` and `/contact/` automatically.

## Launch checklist

1. Replace all placeholders; delete every `class="todo"` block.
2. Deploy and review on the Vercel preview URL.
3. Point `jessicamisener.com` DNS at Vercel; confirm HTTPS.
4. Test the old URLs: `/book`, `/clips`, `/speechwriting`, `/about`, `/contact`.
5. Cancel the Squarespace **site plan** — keep the domain registration.
