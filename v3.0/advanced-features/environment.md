# Environment Management

The Quantum PHP Framework uses an environment-based configuration system to manage settings for different stages of the application lifecycle (e.g., development, production, testing).

## File Selection

The framework selects the environment file based on the `app_env` setting, which is determined during the initial loading phase.

- **Production**: Uses `.env`.
- **Other environments**: Uses `.env.{app_env}` (e.g., `.env.development`, `.env.staging`).

## Lifecycle and Loading

The `Environment` service implements a "one-shot" loading pattern.

### `load(Setup $setup)`

- **One-shot**: Once the environment is loaded, subsequent calls to `load()` are no-ops. 
- **Initialization**: It identifies the target `.env` file, validates its existence, loads the variables, and marks the environment as loaded.

### `env(string $key, $default = null)`

This helper function provides access to environment variables.

- **Contract**: You must call `load()` before accessing any variables via `env()`. If the environment has not been loaded yet, calling `env()` will throw an `EnvException`.

> **Warning**: In long-lived processes (like workers, daemons, or some test suites), be aware that once `load()` is executed, the environment state is fixed. Reloading variables requires the process or the service state to be reset.

## Example

```php
$setup = new Setup('config', 'env', true, 'php');

$env = Di::get(Environment::class);
$env->load($setup);

// Access a variable
$dbHost = env('DB_HOST', 'localhost');
```
