# lyn. — serene.aiart portfolio

A single-page portfolio for lyn., who runs [serene.aiart](https://www.instagram.com/serene.aiart/): a profile column and a bento grid built around the serene.aiart films, drawn live on canvas in a dithered halftone style with hairline vector details.

## Run it

It's one self-contained file. Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
```

## What's inside

- **Profile**: a spinnable planet avatar (drag to spin, tap for night) and a short intro.
- **Films**: each piece has exactly one tile, dithered until you hover, opening in a blurred in-page viewer. The films play one after another; a blue dot marks the one that's on.
- **Now playing**: types out the current film's caption and song credit, has a sound toggle for that film, and a scrubber across all films.
- **Don't blink**: an eye that follows the pointer. Blink it and every film jumps somewhere else.
- **Pace dial**: speeds up or slows down every animation and the films themselves.
- Also Pond and Message me (a small chat box).
- **Sound**: soft chimes made with the Web Audio API, plus the films' own audio. Both can be muted from the footer.

Fonts are Public Sans and Geist Mono from Google Fonts. There are no other dependencies.

## Layout editor (owner only)

You can rearrange and resize the grid yourself, straight on the site.

1. Make a GitHub token: **Settings → Developer settings → Fine-grained tokens → Generate new token**. Under **Repository access**, pick only this repo. Under **Permissions → Contents**, choose **Read and write**.
2. Open the site with `?edit` at the end of the address, for example `https://your-site/?edit`.
3. Paste the token. The page asks GitHub whether that token can write to this repo, and only then turns editing on. Without `?edit` the editor code isn't set up at all, and even with it nothing can be dragged until the token checks out. The token is kept in that browser only (localStorage). "Forget token" removes it.
4. Drag a tile to move it. A ghost shows where it will land, and the other tiles slide out of the way and pack up so there are never overlaps or gaps. Drag any edge or corner of a tile to resize it, from 1×1 up to 4 columns wide and 3 rows tall (Now playing and Message me need at least 2 columns). When you let go, the grid tidies itself so every tile takes the first spot that fits.
5. **Save** commits `layout.json` to this repo. The site reads that file on load, so visitors see the new arrangement once your host serves the new commit.

Notes:
- The editor works on desktop and tablet widths. Phones keep the built-in stacked order.
- It needs the site served from a real address or a local server (`python -m http.server`). The Claude preview link can't reach GitHub and can't pass `?edit`.
- Delete `layout.json` to go back to the default arrangement.

## Placeholders to fill in

- **Message me**: sent with [FormSubmit](https://formsubmit.co), so no server is needed. Set `FORM_TO` near the bottom of `index.html` to your email, send one test message from the live site, and click the confirmation link FormSubmit emails you. FormSubmit then gives you a random address; put that in `FORM_TO` instead so your email isn't in the page. The tile asks for the visitor's message, then their reply email. Until `FORM_TO` is set, it tells visitors their message wasn't sent.
- **Films**: three reels from @serene.aiart live in `art/` and are listed in the `ART` array near the bottom of `index.html`, with their caption and post link. Each entry has an `audio` field for the song credit ("Song · Artist"); it shows next to the title in the captions, Now playing and the viewer. The credits are still empty. To add a piece, drop a video into `art/`, add an entry, and add a film tile with a new `data-i` so no piece repeats.
- The "latest" line in the profile names the newest piece; update it when you post.
