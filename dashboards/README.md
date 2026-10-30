# Home v2 dashboard

A desktop-first redesign of the dashboard, shipped as a **separate** YAML
dashboard so the existing one keeps working untouched.

| View | Path | What changed |
| --- | --- | --- |
| Overview | `/home-v2/overview` | Greeting, presence, weather hero, quick lights, climate, at-a-glance, rooms, media, robots |
| Lights | `/home-v2/lights` | Whole-home row, then one section per floor; room cards show live brightness; scenes |
| Climate | `/home-v2/climate` | Big thermostats, average temperature, per-room chips, 24h trends |
| Weather | `/home-v2/weather` | Closest-city hero, simplified alerts, closest-city forecast, all other cities |
| Robots | `/home-v2/robots` | Vacuum tiles with start/pause/dock controls and battery |
| Media | `/home-v2/media` | TV room + bedroom players, Plex "now playing", network activity |
| Vehicle | `/home-v2/vehicle` | Hero image, remote actions, status, doors/windows |
| Batteries | `/home-v2/batteries` | Grouped by device type, colour-coded, low-battery summary |
| Security | `/home-v2/security` | Alarm panel, cameras, locks, motion, family map |

## Files

```
configuration.yaml        # adds the `lovelace.dashboards.home-v2` entry
dashboards/home.yaml      # the dashboard + button_card_templates
themes/glass.yaml         # dark translucent "Glass" theme
```

## Install

If this repo is the live Home Assistant config directory:

1. Restart Home Assistant (Settings → System → Restart).
   A restart is required because a new dashboard was added; YAML *edits* after
   that only need a browser refresh.
2. Open **Home v2** in the sidebar, or go to `/home-v2/overview`.
3. Keep using the old dashboard from the sidebar at any time.

If HA runs elsewhere, copy the three files to the same relative paths and
restart. The `lovelace:` block is already in `configuration.yaml`.

## Design notes

- **Glass theme** – views set `theme: Glass`, so the redesign does not force a
  theme on the rest of the UI. It is also selectable in your profile.
- **Sections layout** – `column_span` values are chosen for a 4-column desktop
  layout. On a phone the sections stack automatically.
- **Reusable cards** – `glass`, `room`, `person`, `battery`, `sensor` and
  `weather_hero` templates live at the bottom of `dashboards/home.yaml`.
  A new room card is four lines.
- **Dynamic weather** – `sensor.closest_city` carries `condition_entity`,
  `temperature_entity` and `warnings_entity` attributes. The hero and alerts
  read those, so they follow Gervais instead of hard-coding a city.
- **No new custom cards** – only cards already present in the old dashboard are
  used: `button-card`, `mini-graph-card`, `multiple-entity-row`. Built-in
  `tile`, `heading` and `sections` do most of the work.

## Tweaking

- Want a narrower desktop grid? Change `max_columns: 4` to `3` on a view.
- Want a room elsewhere? Move its `custom:button-card` entry between floor
  sections in the Lights view.
- Battery colours are in the `battery` template:
  `< 20%` red, `< 40%` amber, otherwise green.
- If an entity id differs on your instance, find it with:

  ```sh
  grep -oE '\b[a-z_]+\.[a-z0-9_]+' dashboards/home.yaml | sort -u
  ```

## Rollback

Delete `dashboards/home.yaml` and `themes/glass.yaml`, then remove the
`lovelace:` block from `configuration.yaml` and restart. The original
storage-mode dashboard was never modified.
