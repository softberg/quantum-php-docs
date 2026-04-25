# Database

## Overview

The Quantum PHP Framework offers a flexible and powerful database abstraction supporting multiple database systems through adapters. It includes features for connection management, ORM integration, query building, and migrations.

## Supported Database Adapters

- MySQL (via Idiorm)
- SQLite (via Idiorm)
- PostgreSQL (via Idiorm)
- SleekDB (NoSQL key-value store)

## Core Database Class

- Configures and manages the active database connection and ORM adapter based on application configuration.
- Supports connection reuse and lazy connection initialization.
- Provides access to the ORM class for further query and data operations.

## Database Adapters

Adapters implement the specific database logic and ORM integration for each supported technology.
The `IdiormDbal` adapter is the main ORM implementation using Idiorm.

### IdiormDbal Key Features

- Connection setup, including dynamic DSN building.
- Query operator mapping for expressive queries.
- ORM model management and caching.
- Support for transactions, joins, grouping, aggregates.
- Error handling and validation.

## Migrations

Quantum supports database migrations to manage schema changes safely and consistently.
Migration scripts are stored separately and executed via CLI tooling.

## Usage

You can configure the database connection in your config files and use the Database service to interact with data using models and query builders.

```php
$db = new \Quantum\Database\Database();
$orm = $db->getOrmClass();

// Use $orm for queries...
```

## Best Practices

- Keep your configurations environment-aware.
- Use migrations for all database schema updates.
- Encapsulate database logic in models and services.

## Next Steps

Explore:

- [Database Migrations](../advanced-features/migration.md)
- [Models and DbModel](../core-concepts/models.md)
- [Services for database logic](../core-concepts/services.md)
