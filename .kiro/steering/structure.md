# Project Structure

## Root Configuration Files
- `configuration.yaml` - Main Home Assistant configuration with platform integrations
- `automations.yaml` - All automation rules and triggers
- `scripts.yaml` - Reusable script sequences
- `groups.yaml` - Entity groupings for organization
- `scenes.yaml` - Predefined device states
- `customize.yaml` - Entity customizations and UI overrides

## UI Configuration
- `lovelace.yml` - Primary dashboard configuration
- `lovelace-mushroom.yml` - Mushroom theme dashboard variant
- `lovelace-org.yaml` - Alternative dashboard layout

## Organization Patterns

### Configuration Structure
```
configuration.yaml
├── Core integrations (alexa, homekit, influxdb)
├── Platform definitions (light, media_player, sensor)
├── Service configurations (notify, rest_command)
└── Includes (groups, scenes, automations, scripts)
```

### Automation Categories
- **Occupancy-based** - Motion detection and presence automations
- **Lighting control** - Room-specific and timed lighting
- **Climate management** - Temperature and heating control
- **Security** - Door locks and alarm integration
- **Media automation** - TV and entertainment system control
- **Notifications** - Weather, presence, and system alerts

### Entity Grouping Strategy
- **Room-based groups** - `light.bedroom_lights`, `light.kitchen_lights`
- **Floor-based groups** - `light.main_floor_lights`, `light.second_floor_lights`
- **Functional groups** - `light.outdoor_lights`, `group.householdmembers`

## Directory Structure
- `blueprints/` - Reusable automation and script templates
  - `automation/` - Motion sensors, notifications
  - `script/` - Confirmable notifications, device control
- `themes/` - UI theme definitions
- `www/` - Static web assets
- `file_restore/` - Backup configuration files (thermostats)

## Best Practices
- Keep related automations grouped by function or room
- Use descriptive IDs and aliases for all automations
- Maintain consistent entity naming across rooms
- Document complex template logic with comments
- Use blueprints for repeatable automation patterns