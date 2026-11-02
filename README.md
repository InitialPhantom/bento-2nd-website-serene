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
- **Lights on / Lights out**: a dithered eyeball in the middle of its tile that watches the cursor. Click it to switch the whole page to dark mode and back; the label reads Lights on in light mode and Lights out in dark mode, and the choice is remembered in that browser.
- **Pace dial**: speeds up or slows down every animation and the films themselves.
- **Wallpapers**: stills from the films as a fan of dithered cards. Clicking opens a window of square file icons; picking one zooms it into a viewer where the wallpapers glide on a spring with a light motion blur (arrows, drag and flick, mouse wheel, swipe or arrow keys), each with a Download button. Square thumbnails live in `art/wallpapers/thumbs/`; downloads come from `art/wallpapers/jpg/` and save as "serene wallpaper N.jpg".
- **Message me**: a small chat box that opens into a window.
- **Sound**: soft chimes made with the Web Audio API, plus the films' own audio. Both can be muted from the footer.

Fonts are Public Sans and Geist Mono from Google Fonts. There are no other dependencies.

## Layout editor (owner only)

You can rearrange and resize the grid yourself, straight on the site.

1. Make a GitHub token: **Settings → Developer settings → Fine-grained tokens → Generate new token**. Under **Repository access**, pick only this repo. Under **Permissions → Contents**, choose **Read and write**.
2. Open the site with `?edit` at the end of the address, for example `https://your-site/?edit`.
3. Paste the token. The page asks GitHub whether that token can write to this repo, and only then turns editing on. Without `?edit` the editor code isn't set up at all, and even with it nothing can be dragged until the token checks out. The token is kept in that browser only (localStorage). "Forget token" removes it.
4. Drag a tile to move it. A ghost shows where it will land, and the other tiles slide out of the way and pack up so there are never overlaps or gaps. Drag any edge or corner of a tile to resize it, from 1×1 up to 4 columns wide and 3 rows tall (Now playing, Wallpapers and Message me need at least 2 columns). When you let go, the grid tidies itself so every tile takes the first spot that fits.
5. **Save** commits `layout.json` to this repo. The site reads that file on load, so visitors see the new arrangement once your host serves the new commit.

Notes:
- The editor works on desktop and tablet widths. Phones keep the built-in stacked order.
- It needs the site served from a real address or a local server (`python -m http.server`). The Claude preview link can't reach GitHub and can't pass `?edit`.
- Delete `layout.json` to go back to the default arrangement.

## Placeholders to fill in

- **Message me**: sent with [FormSubmit](https://formsubmit.co), so no server is needed. Set `FORM_TO` near the bottom of `index.html` to your email, send one test message from the live site, and click the confirmation link FormSubmit emails you. FormSubmit then gives you a random address; put that in `FORM_TO` instead so your email isn't in the page. The tile asks for the visitor's message, then their reply email. Until `FORM_TO` is set, it tells visitors their message wasn't sent.
- **Films**: four reels from @serene.aiart live in `art/` (04–07.mp4) and are listed in the `ART` array near the bottom of `index.html`, with their caption and post link. Each entry has an `audio` field for the song credit ("Song · Artist"); it shows next to the title in the captions, Now playing and the viewer. The credits are still empty. To add a piece, drop a video into `art/`, add an entry, and add a film tile with a new `data-i` so no piece repeats.
- The "latest" line in the profile names the newest piece; update it when you post.
- **Wallpapers**: the images live in `art/wallpapers/` as 01.webp, 02.webp and so on. To add one, drop in the next number, add a square thumbnail with the same name in `thumbs/` and a JPG copy in `jpg/`, and raise `WALL_N` in `index.html`. The tile previews the first few; the window shows them all with arrows, drag, wheel and swipe.
