# HANDOFF: Open Hardware Guild website, V1

Last updated: 2026-10-08 (deployed to Cloudflare)

## What this is

A one-page static site for the relaunch of Absurd Industries as an open
hardware community for India. The name is **Open Hardware Guild**. The domain is
`openhardwareguild.org`, registered on Cloudflare on 2026-10-08.

The design reuses the absurd.industries kraft-paper look: torn-paper cards, tape, rubber stamps, orange accent, and the fonts
Fraunces, DM Sans and Space Mono.

No build step. Plain HTML, Tailwind from its CDN, and Phosphor icons.

## Files

Everything the public sees lives in `public/`. Only that folder gets uploaded.

- `public/index.html`: the whole site. Sections, in order: hero, why we exist, what we
  do, projects, events, get involved, how we operate, about plus organizers,
  resources, find us, footer.
- `public/style.css`: a trimmed copy of `absurd-industries/style.css`, plus a few
  additions: wordmark sticker, `.slot` placeholder chips, `.img-slot` image
  placeholders, `.example-stamp`, and the past-events photo layout.
- `public/assets/images/`: kraft texture, tape, tools emblem and Absurd logo. All were
  copied from `absurd-industries/hardware-devroom/images/`.
- `public/assets/favicon.svg`: a simple placeholder mark.
- `wrangler.jsonc`: Cloudflare deploy settings. It sets up a Worker named
  `openhardwareguild` that only serves the files in `public/`. It also attaches
  both `openhardwareguild.org` and `www.openhardwareguild.org` to it.
- The page has canonical and og:url tags pointing at `https://openhardwareguild.org/`.

## Hosting

- **Where it runs:** Cloudflare Workers, serving files only, with no server code.
  The account is the single one under balub997@gmail.com.
- **Addresses (all verified serving the page, HTTP 200, 2026-10-08 20:08):** https://openhardwareguild.org, https://www.openhardwareguild.org,
  and https://openhardwareguild.balub997.workers.dev.
- **Deploy:** run `npx wrangler deploy` from the project root. There is no
  automatic deploy on git push yet.
- **Undo a bad deploy:** `npx wrangler rollback`.
- **First deploy:** 2026-10-08, version `988cbb83-f957-41d5-92b0-5fa4a3831f01`.
- **Fragile point:** just after the first deploy, the workers.dev address served
  the page right away. The domain resolved to Cloudflare, but curl failed with
  `sslv3 alert handshake failure`. That means the security certificate was still
  being issued. It clears by itself within minutes. Don't redeploy to fix it.
- **Why not GitHub Pages:** the domain is already on Cloudflare, so this avoids
  any DNS setup. An earlier `CNAME` file for GitHub Pages was removed.

## Status per brief section

| Section | State |
|---|---|
| Hero + why + what we do | Done. Copy follows the brief. A line says we give no grants, equipment or manufacturing. |
| Projects | 3 cards, each stamped "EXAMPLE". Repo and docs links are placeholders. "Share your project" button has no link yet. |
| Events | No upcoming events, as the brief asks. The empty card shows a commented template to copy. "Past" shows 8 real Absurd YouTube recordings, the same set as absurd.industries. |
| Get involved | Done. 6 ways to help. |
| How we operate | 6 principles. The page says the processes behind them don't exist yet. No elections, committees or voting are mentioned. |
| About + organizers | Origin story done. Organizer cards for Balu Babu, Amit and Srinivasan, plus a "this could be you" card. Amit's photo was copied from `absurd-industries/2025/assets/images/amit.jpg`. Balu's was cropped square from a photo he supplied. **Still needed:** a photo of Srinivasan, and profile links for Amit and Srinivasan. Balu links to github.com/balub. |
| Friends of the Guild | Scrolling logo row, copied from "Friends of Absurd". It has the same 7 orgs: PCB Cupid, ampere.works, Vader, Makerville, FOSS United, Mecha, isFixable. Logos are in `public/assets/images/friends/`. **Not yet confirmed with those orgs for the new name.** |
| Resources | Well-known public links: OSHWA, KiCad, FreeCAD, OpenSCAD, Hackaday.io, Adafruit, SparkFun. The page says we don't run them. Two guides are marked "needs a volunteer". |
| Find us | All 5 links are placeholders. No platforms, emails or social accounts were made up. |

## Placeholders to fill

- Search for `#todo`. There are 15 links that need real URLs.
- Search for `[Name]` and `[Project name]`.
- Everything still to fill shows on the page as an orange dashed chip, so you can
  also spot it by eye.

## Defaults chosen where the brief was silent

- **One page, not several.** Each section has an anchor, like `#projects`. This
  is easiest for a few volunteers to edit. Split into pages once projects or
  events get long.
- **Static HTML cards, not a data file.** Adding a project or event means
  copying one block. There are comments above each list saying what to copy.
- **Past events use Absurd recordings.** They are real and already public, and
  they show the community actually builds things. Delete the block if you don't
  want Absurd-era history on the new site.
- **The Absurd Discord is not linked.** The brief says not to assume the
  platform. Add it back in "Find us" if it stays the main channel.
- **Friends list is written once.** A short script at the bottom of
  `index.html` repeats the row so the scroll loops. To add a friend, copy one
  `friend-item` block. The ampere.works logo was shrunk from 6000px (1.7 MB) to
  120px (18 KB).
- **"Bangalore" spelling**, following the brief. absurd.industries says
  "Bengaluru".
- **The wordmark is a CSS paper sticker** reading "Open Hardware Guild", with
  "india" underneath. Replace it with
  an `<img>` once there is a logo.

## How it was verified

- Served with `python3 -m http.server 8765` and captured with headless Chrome at
  1366px wide. Checked each section by eye. All sections render, and the torn
  edges and tape show.
- Phone check: loaded inside a 390px iframe and measured the page width. The
  result was `{"sw":390,"cw":390,"wide":[]}`. That means no sideways scrolling
  and nothing sticking out. Checked the slices by eye. The bottom tab bar shows.
- **Not verified:** a real phone, Safari, and keyboard-only navigation. External
  resource links were not clicked through. Whether the YouTube thumbnails still
  load was only checked in the screenshot, where they loaded.

## Not done

- No real projects, organizers, events or links. Those wait on the team.
- No social preview image (`og:image`).
- Git repo set up locally on `main`, with no commits and no remote. There's no GitHub repo
  and no auto-deploy.
- Optional brief items not built: blog or updates, a separate past-events
  archive page.

## Next steps, in priority order

1. Fill the 5 "Find us" links. Join buttons across the page point there.
2. Add 2–3 real projects. The 6 projects shown in Absurd's hardware devroom are
   obvious candidates, but ask their maintainers first.
3. Add organizer names and photos.
4. Make the first commit, push to GitHub, and connect the repo to Cloudflare
   Workers Builds, so a push to `main` deploys automatically.
5. Make a social preview image.

## Check a change didn't break anything

    cd ~/projects/mix/hardwareguild
    python3 -m http.server 8765 -d public   # open http://localhost:8765, resize to phone width
    npx wrangler deploy --dry-run          # should say "Read 9 files" (more if you add files)
    grep -c '#todo' public/index.html      # links still to fill (15 at V1)
    curl -sI https://openhardwareguild.org/ | head -1   # after deploy: HTTP/2 200
