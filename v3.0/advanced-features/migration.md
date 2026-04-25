# Database Migrations

## Overview

Database migrations provide a way to safely and consistently manage schema changes.
Quantum's migration system supports creating, applying, reverting, and tracking migrations via CLI and programmatic APIs.

## Migration Concepts

- Migrations are PHP classes that contain `up()` and `down()` methods which apply and revert schema changes.
- Migrations are stored in migration files located in the `/migrations` directory.
- A migrations table tracks which migrations have been applied to the database.

## Migration Actions

Supported actions include:
- create
- alter
- rename
- drop

Each action corresponds to templates used in generated migration files.

## Generating a Migration

You can generate a migration file using the CLI:

```bash
php qt migration:create <action> <table_name>
```

Example:

```bash
php qt migration:create create users
```

This creates a migration file with an up/down template for the specified action.

## Applying Migrations

Apply pending migrations with:

```bash
php qt migration:migrate
```

To rollback (downgrade) migrations:

```bash
php qt migration:rollback [steps]
```

## MigrationManager Responsibilities

- Loads migration files and determines which migrations need applying or rolling back.
- Checks for the presence of migration tracking table, and creates it if missing.
- Executes migration classes' `up()` or `down()` methods to apply or revert changes.
- Updates the migrations table with applied and removed migration entries.
- Supports migration ordering and stepping through rollback.

## Best Practices

- Always use migrations for schema changes to keep environments synced.
- Review generated migration templates before applying.
- Use migration rollback during development cautiously.
- Keep migration files under version control.

## Next Steps

Explore related topics:

- [Database](../advanced-features/database.md)
- [Models](../core-concepts/models.md)
- [Services](../core-concepts/services.md)