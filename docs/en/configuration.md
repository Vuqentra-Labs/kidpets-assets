# Configuration

The examples below describe a possible configuration structure. Adjust them to match the plugin implementation.

## General Settings

```yaml
language: en
debug: false
save-interval-seconds: 300
```

## Example Pet Configuration

```yaml
pets:
  axolotl:
    enabled: true
    display-name: "Axolotl"
    role: "Healing and Survival"

    action-passive:
      enabled: true

    need-passive:
      enabled: true
      cooldown-seconds: 60

    active:
      cooldown-seconds: 45

    ultimate:
      cooldown-seconds: 600
```

## Recommended Configuration Rules

- Keep cooldowns configurable.
- Keep messages configurable.
- Allow individual Pets to be disabled.
- Store numerical balance values outside the source code.
- Validate configuration values during plugin startup.
