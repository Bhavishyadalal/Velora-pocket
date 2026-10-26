# Velora Pocket 3.0

A self-contained, mobile-first direct-stream player. Four themes (Velvet, Matcha, Lagoon, Ember), Focus mode, custom touch controls, fullscreen, speed, buffer/picture readouts, optional private history, SRT/VTT subtitles, exposed native audio-track selection, sleep timer, wake lock where supported, sequential-stream guard, exact-URL copying, VLC handoff and tiny M3U playlists.

## Deploy from GitHub to Vercel

1. Create a separate GitHub repository, for example `velora-pocket`. This static player is independent of the Telegram bot; do not replace your bot's files.
2. Upload the contents of this ZIP to the repository root. You should see `public/index.html`, `vercel.json` and this `README.md`. Do not upload the ZIP itself or add an extra wrapping directory.
3. Open https://vercel.com/new and import the repository. Grant Vercel access if it is private.
4. Framework Preset: **Other**. Root Directory: repository root. No install or build command is needed. Output Directory: **public**. The included `vercel.json` configures these values.
5. Deploy, then open the provided HTTPS website on your phone.
6. Paste the complete final HTTPS FSL/R2 or other direct video URL. Tap **Play stream**.
7. Future commits to the connected deployment branch can redeploy the site. You do not need a Python server, a database, a movie bucket, or a background browser for this player.

If you only want to upload one file: rename the local `Velora_Pocket.html` to `index.html`, put it at the root of an otherwise empty repository, and import with Framework **Other**, no build command, Output Directory **.**. Use this as an alternative to the supplied `public/` layout, not mixed with it.

## Use it locally

The `public/index.html` file is identical to `Velora_Pocket.html`. Open either in a full mobile browser. Some file-manager previewers block JavaScript or network media; use Open with → browser. Remote films require internet even though the interface needs no external assets. The file has no external fonts, scripts, poster downloads or analytics code.

## What hosting changes

Vercel serves the player interface. Your phone requests video directly from the media host. The player does not send your pasted URL to a backend, place it in the website address, upload it to GitHub, or proxy the film through Vercel. The site host still receives normal website requests and the media host receives streaming requests.

Clipboard and wake-lock APIs may be more available on a real HTTPS website. Browser permissions and support still apply. HTTPS pages require HTTPS media in this player; HTTP media is rejected with a clear message rather than silently changing a signed URL. A source can also reject embedding or the website's origin.

Preferences and optional history are browser/origin-specific. Your local-file history does not automatically appear on Vercel. Each visitor has separate local browser storage; there is no shared movie library. Private GitHub source visibility does not by itself make the deployed website private. Use Vercel's available deployment access controls if you need website access restrictions; no access-control plan or pricing is promised by this package.

## Real playback limits

A compatible movie starts as data arrives without waiting for a full file download. Watching the entire film still consumes its data, and your browser controls buffering. Pause may continue buffering; **Stop stream** clears the video source to release it.

Browser codec support still determines whether MKV, HEVC, AC3/DTS or multi-track files work. Hosting cannot add codecs, transcode a movie, grant missing server byte-range support, renew expired signatures, or recover removed files. Audio-language selection appears only if the browser exposes actual embedded tracks. Use the exact original URL in VLC for broader format/track support.

Google 10Gbps direct URLs default to sequential mode. No false watch-position resume is attempted; jumps are limited to buffered, seekable video. Other sources can choose Sequential manually. A file whose index is at the end may need VLC or a different source for prompt startup.

Paste the final media URL, not a HubCloud/Greenmotors/gpdl generator page or a Drive share page. Known source-player wrappers can be decoded, but this HTML does not resolve download pages or ads.

SRT/VTT files are read locally. Subtitle timing, size and browser controls are supported. Local subtitle files are not automatically transferred to VLC and must be reselected after reopening the page.

## Controls

- Double-tap the left/right side: skip 10 seconds when available.
- Space/K: play/pause. J/L: −/+10 seconds. Arrows: −/+5 seconds.
- M: mute. F: fullscreen. C: local captions. T: Focus mode.
- Escape: leave expanded player or Focus mode as applicable.
- Focus mode preserves the video element and hides surrounding panels. Leave Focus or use the speed button to access settings again.

## Validation

Validated from a local file and a locally fulfilled HTTPS website with Chromium. Checks include seven viewport sizes, real ranged WebM playback, sequential HTTP 200 playback, safe seeking, local captions, saved-position restore, Stop, VLC URL/playlist handling, all four themes, Focus mode and generic media errors.

No genuine FSL movie URL, physical Android device, native VLC launch, or live Vercel deployment was tested in this environment. The tests use short generated media and fixture responses; no full movie was downloaded. Source availability and device codecs must be checked on your phone.

Vercel static-build reference: https://vercel.com/docs/builds/configure-a-build
