# Fullerton Watch Commander Log

Live civic transparency dashboard for the Fullerton Police Department Watch Commander Log.

**Live site**: https://YOUR_USERNAME.github.io/fullerton-wcl

Data published publicly at `gis.cityoffullerton.com` via ArcGIS Enterprise 11.5 — no authentication required.

## What it shows

| Field | Displayed | Notes |
|---|---|---|
| Incident date/time | ✅ Public | |
| Incident number | ✅ Public | |
| Call type | ✅ Public | Color-coded |
| Location | ✅ Public | Mapped on dark tile |
| Police zone | ✅ Public | Color-coded 1/2/3 |
| Watch commander | ✅ Public | |
| Notifications | ✅ Public | Units notified |
| Priority flag | ✅ Public | |
| **Remarks** | 🔒 **Gated** | Full narrative — requires explicit authorization acknowledgment per CPRA §6254 / PC §293 |

The remarks field contains unredacted narrative text that California law requires to be reviewed before public release. A per-session authorization gate is shown before displaying it.

## Deploy to GitHub Pages

```bash
# 1. Create a new GitHub repo named fullerton-wcl
# 2. Clone it
git clone https://github.com/YOUR_USERNAME/fullerton-wcl
cd fullerton-wcl

# 3. Drop index.html in the root
cp /path/to/index.html .

# 4. Push
git add index.html README.md
git commit -m "Initial deploy"
git push origin main

# 5. Enable GitHub Pages
# → Repo Settings → Pages → Source: Deploy from branch → Branch: main / (root)
# Site will be live at https://YOUR_USERNAME.github.io/fullerton-wcl in ~60s
```

That's it. No build step, no Node, no CI/CD needed.

## Data source

- **Endpoint**: `https://gis.cityoffullerton.com/arcgis/rest/services/Hosted/WatchCommanderLogs/FeatureServer/0`
- **Refresh**: Every 30 seconds
- **Archive**: This single-file version shows the live rolling window (~60 records, ~6 weeks). The rolling window is a deliberate limitation of the city's public endpoint — older records are deleted. For a full historical archive, see the [full AWS/React version](../fullerton-wcl/).

## Legal context

This endpoint is publicly accessible without authentication. Watch commander logs are broadly public record under the California Public Records Act. The remarks field is published without the redactions California law (PC §293, CPRA §6254) requires — this viewer gates that field explicitly and notes the compliance gap.

The City of Fullerton has prior history of misconfiguring public cloud access controls (2019 Dropbox incident, settled for $350K). This is the same pattern on a more sensitive dataset.

Responsible disclosure: `christopher.carter@cityoffullerton.com` (GIS Manager).
