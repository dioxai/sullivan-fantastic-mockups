# Sullivan Fantastic — Promo / Reel Video

## Source
- **Page:** https://sullivanfantastic.com/ (section labeled "— THE REEL — Ninety seconds in the room.")
- **Hosting:** YouTube (embedded via `youtube-nocookie.com`)
- **Video ID:** `BnHRQAGb42M`

## Direct URLs
- **Embed (current usage):** `https://www.youtube-nocookie.com/embed/BnHRQAGb42M?autoplay=1&mute=1&loop=1&playlist=BnHRQAGb42M&controls=0&modestbranding=1&showinfo=0&rel=0&playsinline=1&disablekb=1&fs=0&iv_load_policy=3&cc_load_policy=0`
- **Standard watch URL:** https://www.youtube.com/watch?v=BnHRQAGb42M
- **Standard embed:** https://www.youtube.com/embed/BnHRQAGb42M

## Format
- **iframe-embed** (YouTube). No direct mp4/webm/hls is exposed — YouTube serves DASH/HLS via signed URLs only inside its player. Cannot legitimately hotlink an `.mp4`.

## Poster / Thumbnails (hot-linkable, CORS `*`)
- maxres: https://i.ytimg.com/vi/BnHRQAGb42M/maxresdefault.jpg
- hq: https://i.ytimg.com/vi/BnHRQAGb42M/hqdefault.jpg
- sd: https://i.ytimg.com/vi/BnHRQAGb42M/sddefault.jpg

## Iframe attributes (mirror these)
```html
<iframe
  src="https://www.youtube-nocookie.com/embed/BnHRQAGb42M?autoplay=1&mute=1&loop=1&playlist=BnHRQAGb42M&controls=0&modestbranding=1&showinfo=0&rel=0&playsinline=1&disablekb=1&fs=0&iv_load_policy=3&cc_load_policy=0"
  title=""
  frameborder="0"
  allow="autoplay; encrypted-media; picture-in-picture"
  tabindex="-1">
</iframe>
```
Notes on params: `autoplay=1` + `mute=1` (required for autoplay), `loop=1` with `playlist=<id>` (YT requires the playlist param to loop a single video), `controls=0`, `modestbranding=1`, `playsinline=1`, chrome-stripping flags (`fs=0`, `disablekb=1`, `iv_load_policy=3`, `cc_load_policy=0`).

## Dimensions
- The iframe has no `width`/`height` attributes — sized by CSS on the host page (responsive container). Underlying video aspect appears to be 16:9 (standard YouTube).

## Cross-origin accessibility
- `HEAD https://www.youtube-nocookie.com/embed/BnHRQAGb42M` → HTTP/2 200. Embeddable from any domain (no `X-Frame-Options: SAMEORIGIN` on the nocookie embed path).
- Thumbnail `i.ytimg.com/vi/BnHRQAGb42M/maxresdefault.jpg` → HTTP/2 200, `access-control-allow-origin: *`. Safe to hotlink.

## Recommendation
- **Hotlink the YouTube embed** as-is on the mockup. It's the same asset Chris is using; matches behavior on the live site.
- **Do NOT attempt to download** a raw mp4 from YouTube — it's against YouTube ToS and the URLs are signed/short-lived. If we want a true silent looping background `<video>` (better than the iframe for "hard to see" issues — iframes can't be cropped/object-fit'd well), we'd need to ask Chris for the original master file and rehost it ourselves.
- **No download performed** (no downloadable source exists at the public URL).

## Why Bela might find it "hard to see"
- YouTube iframes don't honor `object-fit: cover`; if the container aspect ≠ 16:9 the video letterboxes or gets cropped by overflow tricks.
- `mute=1` autoplay + `controls=0` means no scrubber/sound — purely ambient.
- For the redesign, requesting the original mp4 from Chris and using a native `<video autoplay muted loop playsinline poster="...">` with `object-fit: cover` would give us full layout control and a crisper hero.
