# promo-assets

Hosts the promo popup config and images for the Overtime Markets app.

Served via GitHub Pages at:
- Config: https://thales-markets.github.io/promo-assets/promo.json
- Images: https://thales-markets.github.io/promo-assets/<filename>

Changes to `main` go live in ~1 minute. **No app deploy needed.**

## Updating a promo

1. Upload the new image (`.webp` / `.png` / `.jpg`) via "Add file → Upload files". Use a unique filename per campaign.
2. Edit `promo.json` — update `image`, `url`, `validUntil`.
3. Commit to `main`.

## Killing a promo

Set `validUntil` to a past ISO date and commit. Propagates within ~5 minutes to open tabs, immediately on new page loads.

## `promo.json` schema

| Field | Type | Description |
|---|---|---|
| `image` | string (URL) | Full URL of the promo image |
| `url` | string (optional) | Click-through target; omit to make the image non-clickable |
| `text` | string (optional) | Caption shown under the image |
| `title` | string (optional) | Modal title |
| `onlyOnce` | boolean | If true, each user sees the promo only once (keyed by image URL) |
| `showForLoggedInOnLoad` | boolean | Show to connected users on page load |
| `guestDisplay` | `"off"` \| `"onLoad"` \| `"onLogin"` | When to show for non-connected users |
| `validUntil` | ISO date string | Popup hides after this date |

## Example

```json
{
  "image": "https://thales-markets.github.io/promo-assets/nba-playoffs-2026.webp",
  "url": "https://www.overtimemarkets.xyz/markets?status=OpenMarkets&sport=Basketball",
  "text": "",
  "title": "",
  "onlyOnce": true,
  "showForLoggedInOnLoad": true,
  "guestDisplay": "onLoad",
  "validUntil": "2026-04-21T10:00:00"
}
```

## Gotchas

- **Always use a unique image filename per campaign.** The app uses the image URL as the "seen" key in localStorage — reusing a filename means users who saw the previous promo won't see the new one.
- **Image size**: keep under ~500 KB for fast loading. `.webp` is preferred.
- The `promo.json` file must always exist and be valid JSON. If fetch fails, the popup simply won't show (no user-facing error).
