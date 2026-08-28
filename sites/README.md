# Client websites

Two independent static sites. Each folder is a complete website — one
self-contained `index.html` (all CSS and JS inlined) plus an `assets/`
folder for images.

    sites/
      ms-beauty-clinic/   → Ms Beauty Clinic, Leixlip, Co. Kildare
      aphros/             → Aphrós Massage & Beauty, Gorey, Co. Wexford

---

## Deploying to Netlify

Both sites live in this one repo, so each gets its own Netlify site pointed
at a different **base directory**. Repeat these steps twice.

1. **netlify.com → Add new site → Import an existing project → GitHub**,
   authorise, and pick this repository.
2. **Base directory** → `sites/ms-beauty-clinic` (or `sites/aphros`).
   **Build command** → leave empty. **Publish directory** → `.`
   The `netlify.toml` in each folder already sets this.
3. **Deploy.** You get a live `*.netlify.app` URL straight away.
4. **Domain management → Add a domain** → follow the DNS instructions.
   SSL provisions automatically and is free.
5. **Forms → Form notifications → Add notification → Email notification.**
   Point it at the client's inbox. This is what makes the contact form work —
   without step 5 submissions are captured but nobody gets emailed.

Every later change: push to this branch and the site rebuilds automatically.

## Forms

Each site has one Netlify form (`enquiry` on Ms Beauty, `booking` on Aphrós).
They need no backend — Netlify detects `data-netlify="true"` at deploy time,
handles the POST, stores the submission and emails whoever is configured in
step 5. Both include a honeypot field for spam.

Free tier covers roughly 100 submissions per month per site; check the current
limit when signing up.

## Replacing images

Every image is currently a styled placeholder:

    <div class="ph" data-label="Hero image — therapist in clinic"></div>

Drop the real photo into that site's `assets/` folder and swap the div for:

    <img src="assets/hero-therapist.jpg" alt="Descriptive alt text">

The surrounding CSS handles sizing. Each placeholder has an HTML comment
directly above it naming the suggested filename.

## Outstanding content

Search each `index.html` for `CONFIRM` — every value still needing sign-off
from the client is tagged, and listed in a block comment at the top of the file.
