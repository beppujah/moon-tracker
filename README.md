# Moon Mood

See where the Moon is right now, and find out whether your mood follows its phases.

**Open the app: https://beppujah.github.io/moon-tracker/**

Moon Mood runs in the browser and works best on a phone. Point it at the sky and the Moon stays in place on screen while you move. Log how your day went, and after a couple of lunar cycles the app tells you whether there is any real link between your mood and the Moon.

## Features

**Sky**
- Real-time azimuth, altitude, distance and phase for your location
- Gyroscope and compass view: turn the phone and the Moon stays fixed in the sky
- Correct orientation of the lit side, as you see it from where you stand
- Moonrise and moonset, next New or Full Moon, Sun position and bright stars
- Time slider to move up to 72 hours forward or back

**Mood**
- One tap a day on a five-step scale: Awful, Bad, Okay, Good, Great
- Optional note; past days can be filled in too
- The Moon's phase and illumination for each day are saved with the entry

**Report**
- Average mood for each of the eight lunar phases
- Mood plotted against the Moon's illumination, with a trend line
- Pearson correlation and a permutation-test p-value, with a plain-language verdict
- Sample data preview, so you can see the report before you have your own

## Use it on your phone

1. Open https://beppujah.github.io/moon-tracker/ in your phone's browser.
2. Add it to your Home Screen to use it as a full-screen app: on iPhone tap **Share → Add to Home Screen**; on Android open the browser menu and tap **Add to Home screen**.
3. Tap **Enable sensors** and allow motion and location access.
4. Point the phone at the real Moon and tap **Align to Moon** to correct the compass.

The Home Screen app keeps its own data, separate from the browser, so log your mood from the same one every time.

## Privacy

No account, no server, no tracking. Entries are stored only in your browser on your device. Use **Export CSV** in the Mood tab for backups, and **Import CSV** to restore them.

## How it works

| Part | Method |
|---|---|
| Moon position | Truncated lunar series from Jean Meeus, *Astronomical Algorithms* (ch. 47), with topocentric parallax and atmospheric refraction. Accurate to a few tenths of a degree. |
| Phase and lit side | Phase angle and bright-limb position angle, rotated by the parallactic angle for your location |
| Sun | Low-precision solar coordinates |
| Orientation | DeviceOrientation API (absolute heading where available, `webkitCompassHeading` on iOS), magnetic declination correction and manual alignment |
| Statistics | Pearson's r between mood (−2 to +2) and illuminated fraction; p-value from a 2,000-shuffle permutation test |

The whole app is a single `index.html` with no build step and no libraries. The only external resource is the Geist font from Google Fonts. A small service worker (`sw.js`) keeps a copy of the app on the device, so once opened it also works offline.

## Limitations

- Compass accuracy depends on the phone's magnetometer and can be off by several degrees near metal or electronics. Use **Align to Moon** to fix it.
- Motion and location sensors only work over HTTPS, which GitHub Pages provides.
- A correlation over a few weeks of data is weak evidence. The report says so until you have at least two lunar cycles (about 59 days).

## Files

| File | Purpose |
|---|---|
| `index.html` | The app |
| `manifest.webmanifest` | Name and icons for Add to Home Screen |
| `sw.js` | Service worker: offline use and the browser's Install prompt |
| `apple-touch-icon.png`, `icon-192.png`, `icon-512.png` | App icons |
