# Tropical cyclones in 3D, updated daily

A GitHub Pages site that shows a 3D flow animation for every active tropical cyclone on Earth,
rebuilt every morning by GitHub Actions. It also serves as a portfolio page (edit `site/config.js`).

**What happens each day** (`.github/workflows/update.yml`, 06:40 UTC)

1. `scripts/storms.py` reads NCEP TCVitals from the last 8 days of GFS cycles. TCVitals carries the
   operational position and intensity of every active storm (NHC, CPHC, JTWC, ...), so this covers
   all basins and gives each storm's official track. Invest areas (90–99) are skipped.
2. `scripts/run_daily.py` downloads GFS 0.25° analyses (u, v, omega, vorticity, 900–500 hPa) for each
   storm's region, renders the video with `tc3d/render.py`, and deletes the data and frames at once.
3. Videos of storms that have ended are copied forward from the live site into the archive.
4. Only `public/` (web page, MP4s, posters, `storms.json`) is uploaded to GitHub Pages.
   No data or video is ever committed to the repository.

## The website: a single-screen dashboard

- **Storms (left)**: active storms with intensity sparklines and basin filters, pinned storms, and
  storms that recently ended.
- **Stage (centre)**, four views: a WebGL **globe** (NASA Blue Marble and Black Marble, real day and
  night), the **3D flow** video, a **track map**, and **compare** (two videos side by side).
- **Shared timeline (bottom)**: storm lifespans, official intensity, rapid-intensification periods and
  the 3D video window. One playhead drives everything: storm positions on the globe, the video
  frame, the map, and every number in the inspector. Play, step an hour, change speed.
- **Inspector (right)**: wind, 24-hour change, motion, pressure, deep and mid-level shear, humidity,
  SST, tilt and radius of maximum wind at the playhead's hour, each with a sparkline; a live
  checklist of conditions often linked to rapid intensification; the written summary; downloads and a
  NASA Worldview link for the same hour.
- **Search** (Ctrl K), **pins**, deep links (`#storm=2026_17E&view=flow`), keyboard shortcuts
  (space, ← →, [ ], 1–4), and drawers for the season summary, archive, guide and About.

## Notes

- Rapid intensification is flagged only from the official intensities (increase of at least
  30 kt in 24 h), never from GFS winds.
- Southern Hemisphere storms are handled (vorticity sign flipped), and so are storms crossing 180°.
- GitHub Pages sites are limited to about 1 GB; each video is roughly 5–15 MB, which is why the
  archive is capped.
- This is a research visualisation, not a forecast.
