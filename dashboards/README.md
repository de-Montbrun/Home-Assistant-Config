# Home v2

A copy of the existing dashboard with the **Glass** theme applied, registered
as a second YAML dashboard so it can be tested before anything is swapped.

## What it is

- `dashboards/home.yaml` - the current dashboard's cards, unchanged apart from
  one `theme: Glass` line per view. Generated from
  `backups/dashboard-old.yaml` (Jan 2026 export).
- `themes/glass.yaml` - the theme: graphite surfaces, soft periwinkle accent,
  amber for "on" states, backdrop blur on cards.
- `configuration.yaml` - registers `home-v2` (sidebar: **Home v2**).

URL: `/home-v2/dashboard` (and `/home-v2/lights`, `/home-v2/robots`, ...).

## Install / test

1. `git pull`
2. Restart Home Assistant (required, new dashboard was registered).
3. Open **Home v2** in the sidebar. The existing dashboard is untouched.

After the first restart, edits to `dashboards/home.yaml` only need
**Refresh** from the dashboard's three-dot menu.

## Swap it in for the real dashboard

When you're happy with it:

1. Rename the dashboard key/title/icon in `configuration.yaml` if you want it
   to read as "Home".
2. Remove the old UI-managed dashboard in **Settings > Dashboards**.
3. Optionally set Home v2 as the default dashboard.

## If your live dashboard has changed since Jan 2026

The file was built from the January export. To refresh it from the live one:

1. Open the current dashboard > **Edit** > three dots > **Raw configuration
   editor** > copy everything.
2. Paste it over `dashboards/home.yaml`, then add `theme: Glass` under each
   view (one line, same indentation as `path:`).
3. Commit/push, then Refresh the Home v2 dashboard.

## Rollback

Delete `dashboards/home.yaml`, remove the `lovelace:` block from
`configuration.yaml`, restart. `themes/glass.yaml` can stay - it is harmless
until selected, and is also available in User profile > Appearance.
