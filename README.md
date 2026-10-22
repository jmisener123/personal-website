# jessicamisener.com

Personal site for Jessica Misener — writer, editor, AI product builder.

Plain HTML and CSS. **No build step, no dependencies, no `npm install`.** Edit a
file, push, and Vercel deploys it. It will still work in ten years.

## Files

```
index.html            Home
about/                Bio, caption contest wins, photo
writing/              Landing: books + selected clips
writing/books/        Both books
work/                 AI & product work, talks
contact/              Contact form + email, LinkedIn, GitHub
thanks/               Post-submit landing page (noindex)
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

**Add a clip:** open `writing/index.html`, copy an existing `<li>` block in the
"Selected clips" list, and fill in the title, link, and outlet. Keep the list
short — it's a highlight reel, not an archive. Clips live only on this page;
there's no separate clips page.

**Add a project:** copy a `<li class="card">` block in `work/index.html`.

**Add a page:** create `newpage/index.html` (a folder with an `index.html` gives
you the clean `/newpage/` URL), copy the header and footer from any existing
page, and add a `<url>` entry to `sitemap.xml`.

**Change the nav or footer:** these are duplicated across all nine HTML files —
the one real cost of skipping a build step. Search and replace across the repo.
On the current page, that page's nav link carries `aria-current="page"`.

## The contact form

`contact/index.html` posts to [Web3Forms](https://web3forms.com) — no backend,
no JavaScript, no account. Setup is one step:

The access key is already in the form's hidden `access_key` field, so it works
as soon as the site is deployed. Submissions are emailed to the address
registered with Web3Forms. The key is safe to commit: it
only permits sending mail *to* you, and it does not expose your address.

Hidden fields: `subject` sets the email subject, `from_name` labels the sender,
`redirect` is where the visitor lands afterward (`/thanks/`), and `botcheck` is
a honeypot — leave it alone.

**On privacy:** there are no `mailto:` links anywhere on the site, so your
address is never published. The form is the only way to reach you, and the
access key does not reveal where mail is delivered.

## Before launch

No placeholder callouts or `[square brackets]` remain — the site is
content-complete for a barebones launch, and the contact form's access key is
in place. Send yourself one real test message from the deployed site before
cutting over DNS.

Also confirm the LinkedIn and GitHub URLs and the copyright year.

**The email address appears nowhere on the site, by design.** There are no
`mailto:` links; the contact form is the only route. Web3Forms delivers to the
address you register with them, and the access key in the page source does not
expose it. If you ever add a `mailto:` link, you undo this.

Nothing was invented. The book copy and bio were recovered from the old
Squarespace site and edited; the clips on `writing/index.html` are real and
link-checked. The Work page deliberately carries no project case studies rather
than fake ones — add them when you want it to.

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

1. Add your Web3Forms access key (see above).
2. Deploy and review on the Vercel preview URL.
3. Submit the form as a test and confirm the message reaches you.
4. Point `jessicamisener.com` DNS at Vercel; confirm HTTPS.
5. Test the old URLs: `/book`, `/clips`, `/speechwriting`, `/about`, `/contact`.
6. Cancel the Squarespace **site plan** — keep the domain registration.
