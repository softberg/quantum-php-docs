# Configuration

## Overview

The Quantum PHP Framework provides a powerful and flexible Configuration system that manages application settings across different environments and modules.

The configuration system loads, merges, and manages settings using a layered approach with support for environment overrides, file imports, and dot-notation access.

## Key Features

- Centralized storage of all configuration data using a dot-accessible data container.
- Loading and importing config files with collision detection.
- Access, set, remove, and flush config values at runtime.
- Support for environment-specific configurations.
- Integration with Quantum's Dependency Injection (DI) container for loading.

## Configuration Loading

Configurations are loaded via `Quantum\Loader\Loader` based on a `Setup` descriptor that describes which files and environment apply.
The `Config` class manages this process and the in-memory data structure.

## API Methods

- `load(Setup $setup)`: Load all configuration files.
- `import(Setup $setup)`: Import additional config files.
- `get(string $key, $default = null)`: Retrieve a config value.
- `has(string $key)`: Check if config key exists.
- `set(string $key, $value)`: Set or overwrite config value.
- `delete(string $key)`: Remove a config key.
- `flush()`: Clear all loaded config data.
- `all()`: Retrieve all configs as dot-accessible object.

## Environment Support

Configurations can be environment-specific by loading different files or values based on environment variables.

## Usage Examples

```php
// Retrieve a config value
$appName = config()->get('app.name', 'Quantum Application');

// Set a config value at runtime
config()->set('mailer.smtp.host', 'smtp.example.com');

// Check if config key exists
if (config()->has('database.default')) {
    // Do something
}
```

Other framework components frequently use the config system to determine behavior, such as routing prefixes, mail settings, logging verbosity, caching backends, and more.

## Best Practices

- Organize config files per module for maintainability.
- Use environment overrides to separate dev, staging, and production configurations.
- Avoid hardcoding values in code; prefer config injection.

## Next Steps

For broader understanding, explore:

- Dependency Injection for configuration management.
- Module-level configuration.
- Environment and server variable management.

