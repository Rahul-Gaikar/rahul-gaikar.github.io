# Rahul Builds: project notes for Claude

Rahul Gaikar's builder site: what he designs, builds and ships. Live at **https://rahul-gaikar.github.io** (GitHub Pages, served from the `main` branch).

Rahul is a product designer, not a developer. Talk to him in plain words, show changes visually, and never make him touch code.

## How we work

- **Two tracks**
  - `main` = the live site. Changes are previewed first and pushed only when Rahul says **"publish"**.
  - `v2` = the experimental redesign ("v2 Lab"). Iterate freely; never merge into `main` until Rahul says **"ship v2"**.
  - If a request doesn't say which track, ask.
- **Preview first.** Run the site locally (any static server, e.g. `npx serve .`) and show Rahul screenshots at phone (390px) and laptop (1200px) widths, in light and dark. Push only after he approves.
- **Keep content in sync.** Content changes made on `main` (projects, stats, goal numbers) must be copied to `v2` too.
- **Never invent facts.** No made-up stats, dates, testimonials or prices. If something is missing, ask, or hide that element until real data exists.
- Plain static site: HTML, CSS and JS in each page. No build step, no framework.

## Files

| File | What it is |
|---|---|
| `index.html` | Home page. All home content is in the `SITE` object near the bottom (projects, intro, building-now, etc.). |
| `support.html` | Support page: UPI payments (amount chips, QR on laptops, "Pay with UPI" button on phones) and the monthly Claude goal. Its settings are in the `SUPPORT` object. |
| `goal.js` | **Single source** for the monthly Claude goal (`target`, `raised`, `supporters`, `updated`). Used by the home-page goal card and the support page. |
| `avatar.webp` | Profile picture (illustrated). |
| `favicon.svg`, `apple-touch-icon.png` | "R with a green dot" icon. |

### Common updates (edit content only, don't touch the rendering code)

- **Mark a project live / add one:** edit `SITE.projects` in `index.html`. Status values: `shipped`, `live`, `building`, `next`.
- **Glowfinder stats:** `SITE.projects[0].stats` (`visits`, `signups`, `daily[]`, `source`).
- **Support money came in:** update `raised`, `supporters` and `updated` in `goal.js`. Reset at the start of each month when Rahul asks.
- **"Updated" date** in the footer: `SITE.updated`.

## Design rules

- Colours: background `#F4F5F7`, ink `#14161A`, cobalt accent `#2B44FF` (links, the "Motion for hire" block), green `#1B8F4D` = shipped/live, amber `#C77A00` = building. Dark mode has its own token values in `:root`.
- **Claude orange `#D97757`** is used **only** for support/Claude-goal elements. Use the deeper `#B85433` behind white text so it stays readable.
- Fonts: headings Bricolage Grotesque, body Newsreader (Google Fonts).
- Motion: calm and springy, always respecting `prefers-reduced-motion`.
- **Don't draw other companies' logos** (no Claude/Anthropic logo, no social-network logos); use text labels or original marks. The "spark" on the support page is an original four-point star.
- Theme: light/dark toggle (remembered per visitor) with a top-to-bottom blur-sweep transition and an animated sun/moon icon.

## Live site (`main`) currently has

Top bar with avatar + "Rahul Builds", links and theme toggle; a two-line mobile menu (dropdown card); projects: **Glowfinder** (new, with visits/sign-ups sparkline), Hourglass, Orbito 3D, Bucket List; "Before this" (Port); "Motion for hire" (links to motionbyrahul.framer.website); "Say hello" with email + copy button and the orange Claude-goal card; footer with avatar, one-liner and social pills (X, YouTube, Instagram, GitHub).

## v2 Lab (`v2`) currently has

- **Nav:** profile pill on the left (turns into a "you are here" label with a rolling section-name animation on scroll); links tuck into a **progress circle** on the right; hover/tap the circle to fan them out. When the open bar would touch the profile pill (small screens), the two **merge like liquid** (SVG goo filter) into one container. On the narrowest phones the avatar melts into the bar.
- **Projects as an expandable list** with smooth height animation; a hover-preview system is wired in (`media: { type: "image" | "video", src, poster, alt }` per project) and turns on once visuals exist.
- **"Building now"** section above the list: Hourglass 3D, collapsible, with a stats area (milestones + waitlist) that stays hidden until real data is added.

## Open items (ask Rahul)

1. **Project visuals** for the hover previews: a screenshot or a 3–6 s muted MP4 (under ~2 MB) per project, stored in a `media/` folder.
2. **Wider layout (planned, approved in principle):** page width steps up with the screen (full width on phones, ~56rem on laptops, ~68rem max on large screens), with a two-column layout on big screens (sticky section titles on the left, content on the right). Paragraphs stay capped at ~34rem.
3. **Hourglass 3D:** co-founder's name and link for the credit line, milestones, waitlist link and count.
4. **Support page in v2** still uses the old top bar; give it the new nav.
5. The second Miscrits app (spawn locations + search counter) can be added once Rahul shares its name, link and status.
6. Exact launch months for Hourglass and Orbito 3D (only needed if a layout shows dates).

## Git

- Push with `git push origin <branch>`. Check the live build with `gh api repos/Rahul-Gaikar/rahul-gaikar.github.io/pages/builds/latest`.
- Old versions are in the history; to roll back, restore a previous commit when Rahul asks.
