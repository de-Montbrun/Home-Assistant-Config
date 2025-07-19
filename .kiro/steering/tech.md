# Technology Stack

## Platform
- **Home Assistant Core** - Primary automation platform
- **YAML Configuration** - Declarative configuration approach
- **MQTT** - Message broker for device communication
- **Zigbee2MQTT** - Zigbee device integration

## Key Integrations
- **InfluxDB** - Time series data storage and analytics
- **Alexa Smart Home** - Voice control integration
- **HomeKit** - Apple ecosystem integration
- **Mobile App** - iOS notifications and control
- **Plex Media Server** - Media automation triggers
- **Weather Services** - Multiple Canadian city weather data
- **Wemo** - Smart switch integration (static IP configuration)

## Development Conventions

### YAML Style
- Use 2-space indentation consistently
- Vim modeline: `# vim: set expandtab tabstop=2 shiftwidth=2 softtabstop=2:`
- Organize with folding markers `# {{{ Section }}}` and `# }}}`
- Use `!include` directives for modular configuration

### Entity Naming
- Use descriptive, location-based names (e.g., `light.bedroom_ceiling`)
- Group related entities with consistent prefixes
- Create light groups for room-level control

### Secrets Management
- Store sensitive data in `secrets.yaml` using `!secret` references
- Never commit actual credentials or API keys

## Common Commands

### Configuration Validation
```bash
# Check configuration syntax
hass --script check_config

# Restart Home Assistant
sudo systemctl restart home-assistant
```

### Development Workflow
- Test automations in Developer Tools before deployment
- Use template editor for complex Jinja2 expressions
- Validate YAML syntax before committing changes