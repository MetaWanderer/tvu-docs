# TVU Docs — Production Schedule Reference

Hosted at: **https://metawanderer.github.io/tvu-docs/**

---

## How to spin up a new shoot schedule (fast path)

1. Duplicate `shilo.html` and rename it (e.g. `deion.html`)
2. Find + replace the 5 things below
3. Commit and push — page is live in ~60s

---

## The 5 things to update

### 1. Shoot date & timezone
```js
const ET_OFFSET = 4;              // EDT (Apr–Oct) = 4, EST (Nov–Mar) = 5
const SHOOT_DATE = [2026, 3, 30]; // [year, month-1 (JS 0-indexed), day]
// April = 3, May = 4, June = 5, July = 6
```

### 2. Hero title + label
```html
<div class="hero-label">TVU PACK — MIAMI IRL</div>       <!-- shoot context -->
<h1 class="hero-title">Shilo Sanders Shoot</h1>           <!-- talent name -->
<p class="hero-sub">Miami, FL · Thursday, April 30</p>    <!-- city + date -->
```

### 3. Pack PID + stream URL (hero strip)
```html
<span ... id="packPid">C6B13F6BFB7FF216</span>           <!-- from Slack canvas SSS Details -->
<span ...>twitch.tv/shilosanders</span>                   <!-- primary stream channel -->
```

### 4. Quick-links (hero pills)
```html
<a href="https://www.twitch.tv/shilosanders">Shilo — Twitch</a>
<a href="https://www.instagram.com/joeyjoy">JoeyJoy — Guest</a>
<a href="tel:7199673071">Dominick — POC</a>
<a href="tel:7204851721">Shilo — Direct</a>
```

### 5. Timeline blocks
Each block has `data-start` / `data-end` (24h ET) — the page auto-highlights the current block:
```html
<div class="tl-block" data-start="11:00" data-end="11:30">
  <div class="tl-time">11:00</div>
  <div class="tl-card shilo-card">
    <span class="tl-tag shilo-tag">SEGMENT 1 — BACON BITCH</span>
    <div class="tl-name">Brunch — Bring Your Chat Along</div>
    <div class="tl-desc">Description here...</div>
    <!-- address block (optional) -->
    <div class="tl-addr">
      <span class="tl-addr-text">ADDRESS HERE</span>
      <button class="copy-btn" onclick="copyText(this,'ADDRESS HERE')">Copy</button>
      <a class="map-btn map-apple"  href="https://maps.apple.com/?q=ADDRESS">Maps</a>
      <a class="map-btn map-google" href="https://maps.google.com/?q=ADDRESS">Google</a>
      <a class="map-btn map-waze"   href="https://waze.com/ul?q=ADDRESS&navigate=yes">Waze</a>
    </div>
    <div class="tl-badges">
      <span class="tl-badge badge-live">LIVE</span>
      <span class="tl-badge badge-feat">45–60 min</span>
    </div>
  </div>
</div>
```

---

## Color themes (swap per talent/shoot)

| CSS var | Default | Use for |
|---|---|---|
| `--shilo` / `--shilo-bg` | `#60a5fa` blue | Talent A / brunch segments |
| `--gym` / `--gym-bg` | `#c084fc` purple | Gym / high-energy location |
| `--tennis` / `--tennis-bg` | `#34d399` green | Passion segment / final location |
| `--green` | `#70b858` TVU green | Crew / rules / positive callouts |

To change theme for a new talent, just swap the hex values in `:root` at the top of the file.

### Card class → color mapping
```
shilo-card / shilo-tag  →  --shilo  (blue)
gym-card   / gym-tag    →  --gym    (purple)
tennis-card/ tennis-tag →  --tennis (green)
drive-card / drive-tag  →  --orange (orange) — always used for drives
setup-card / setup-tag  →  --text-dim (gray) — crew call, wrap
```

### Badge classes
```
badge-live   — green  LIVE
badge-tbd    — gray   Maybe Stream
badge-off    — gray   Off Stream
badge-feat   — blue   feature callout (time, feature name)
```

---

## Crew section
```html
<div class="crew-av" style="background:var(--green-bg);color:var(--green);">S</div>
<div class="crew-name">Socrates</div>
<div class="crew-role">Technical Production · Director</div>
```
Avatar initials, name, role. Add `<span class="crew-gear-tag">Sony FX3 · S-Log3</span>` for camera ops.

---

## Address blocks — map deep links

All three open their native app on mobile (Safari/Chrome prompt):
```
Apple Maps: https://maps.apple.com/?q=ENCODED_ADDRESS
Google Maps: https://maps.google.com/?q=ENCODED_ADDRESS
Waze:        https://waze.com/ul?q=ENCODED_ADDRESS&navigate=yes
```
Encode spaces as `+` in the URL.

---

## Deploying an update

```bash
cd /Users/socrateslozano/Desktop/TVUSource/docs
git add shilo.html          # or whatever file changed
git commit -m "Update Shilo schedule — add confirmed address"
git push
```
Live in ~60 seconds at `https://metawanderer.github.io/tvu-docs/[filename].html`

---

## Files in this repo

| File | What it is |
|---|---|
| `shilo.html` | Shilo Sanders Miami IRL shoot — April 30, 2026 |
| `index.html` | GO App LA Field Day shoot — Feb 20, 2026 |
| `GO-App-LA-Field-Day.html` | Field Day alternate |
| `GO-IRL-Pickups-ShotSheet.html` | IRL pickups shot sheet |
| `scribes/PRORig-FX3-FX30-Build-Guide.html` | FX3/FX30 rig build guide |
| `scribes/Sony-HDMI-Output-Settings.html` | Sony HDMI settings reference |

---

## Source of truth

Shoot details always come from the **Slack canvas** linked in the shoot channel.  
Canvas → SSS Details section has: Pack PID, contacts, stream URL.  
Never invent production language — pull it directly from the canvas copy.
