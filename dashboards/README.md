# Home v2

Your current dashboard, unchanged, plus the **Glass** theme. Registered as a
second YAML dashboard so it can be tested before anything is swapped.

## What it is

- `dashboards/home.yaml` - the live dashboard copied verbatim (11 views:
  Dashboard, Lights and Switches, Robots, Climate-control, Climate, Weather,
  Media Players, Vehicle, RAM 1500, Security, Alarm), plus one `theme: Glass`
  line per view and the `button_card_templates` block.
- `themes/glass.yaml` - frosted graphite theme: translucent cards with a real
  backdrop blur, soft periwinkle accent, amber for "on" states.
- `configuration.yaml` - registers `home-v2` (sidebar: **Home v2**).

URL: `/home-v2/dashboard`, `/home-v2/lights`, `/home-v2/robots`, ...

Only intentional deviation from the source dashboard: the Security quick-action
button navigates to `/home-v2/security` instead of `/lovelace/security`.

> **Themes are set per view, not per dashboard.** A `theme:` key at the top of a
> dashboard config (next to `views:`) is silently ignored by Home Assistant.
> It has to go inside each view, as a sibling of `path:`/`cards:`. The only
> dashboard-wide alternative is the per-user theme in
> **User profile > Appearance > Theme**.

## Install / test

1. `git pull`
2. Restart Home Assistant (required, new dashboard was registered).
3. Open **Home v2** in the sidebar. The existing dashboard is untouched.

After that, edits to `dashboards/home.yaml` only need **Refresh** from the
dashboard's three-dot menu.

## Swap it in for the real dashboard

1. In `configuration.yaml`, rename the key/title/icon if you want it to read
   as "Home" instead of "Home v2".
2. Remove the old UI-managed dashboard in **Settings > Dashboards**.
3. Optionally set Home v2 as the default dashboard.

If you rename the key, also update the Security button's
`navigation_path` to `/<new-key>/security`.

## Keeping it in sync with the live dashboard

The live dashboard is UI-managed (stored in `.storage/`, not in git). When you
change it there, refresh this copy:

1. Open the dashboard > **Edit** > three dots > **Raw configuration editor**.
2. Copy everything.
3. Paste over `dashboards/home.yaml` and add `theme: Glass` under each view
   (one line, same indentation as `path:`).
4. Commit/push, then Refresh the Home v2 dashboard.

## Getting the new buttons on your existing dashboard

`button_card_templates` belong to a dashboard, not to a theme. Selecting Glass
in your profile restyles everything the theme controls (surfaces, colours,
spacing) but leaves the old quick-action buttons alone, because their styling
is written in the dashboard's own templates.

To match Home v2:

1. Open your dashboard > **Edit** > three dots > **Raw configuration editor**.
2. Replace the `button_card_templates:` block at the very bottom with the one
   at the end of `dashboards/home.yaml`.
3. Save. No restart, no theme reload needed.

The block uses literal colour fallbacks (`var(--x, #hex)`) so it still looks
right if you switch to a theme that does not define the Glass variables.

## Rollback

Delete `dashboards/home.yaml`, remove the `lovelace:` block from
`configuration.yaml`, restart. `themes/glass.yaml` can stay - it is harmless
until selected, and is also available in User profile > Appearance.
