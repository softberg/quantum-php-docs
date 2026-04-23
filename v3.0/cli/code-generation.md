# Code Generation

In the current Quantum PHP Framework command set, code generation is mainly centered around creating modules and migrations.

So this page should not talk about generation in a vague framework sense. It should describe what `qt` actually generates today.

## What `qt` currently generates

From the upstream core commands, the main generation commands are:

- `php qt module:generate`
- `php qt migration:generate`

That means the current code generation story is primarily about:

- generating new modules from templates
- generating new migration files

## Module generation

The main scaffolding command is:

```bash
php qt module:generate Blog
```

This command creates a new module using a template.

From the upstream `ModuleGenerateCommand`, it accepts:

- a required module name argument
- `--template` or `-t`
- `--yes` or `-y`
- `--with-assets` or `-a`

A more explicit example looks like:

```bash
php qt module:generate Blog --template=DefaultWeb --with-assets
```

## What `module:generate` actually does

From the upstream `ModuleManager`, module generation does real framework work, not just file copying.

It:

- ensures the `modules/` directory exists
- loads files from a module template
- processes template placeholders such as module namespace and module name
- writes the generated files into `modules/<ModuleName>/`
- optionally copies template assets into the assets directory
- updates `shared/config/modules.php`

So this command is important because it creates a framework-ready module and also registers it in project configuration.

## Available module templates

From the current upstream core templates, the available module templates are:

- `DefaultApi`
- `DefaultWeb`
- `DemoApi`
- `DemoWeb`
- `Toolkit`

This matters because `module:generate` is not one fixed scaffold. The template changes what kind of module structure you start with.

## What a generated module can include

Depending on the selected template, a generated module can include things such as:

- controllers
- routes
- middlewares
- views
- services
- other module files
- optional assets when `--with-assets` is used

So module generation is the real center of scaffolding in Quantum right now.

## Migration generation

The second generation command is:

```bash
php qt migration:generate create posts
```

From the upstream `MigrationGenerateCommand`, this command requires:

- an action
- a table name

The supported action flow is described in the command as:

- `create`
- `alter`
- `rename`
- `drop`

So another valid example would be:

```bash
php qt migration:generate alter posts
```

## What `migration:generate` does

This command creates a new migration file through `MigrationManager`.

Its job is focused and specific:

- generate the migration file name
- create a new migration file for the given action and table

That makes it part of Quantum's code generation story, even though it is more narrow than module scaffolding.

## What code generation does not currently mean

Based on the current upstream command set, the docs should be careful not to imply that `qt` currently generates every framework piece individually.

For example, the current built-in commands do not show separate generators like:

- `controller:generate`
- `middleware:generate`
- `view:generate`

Those pieces are typically created through module templates, not through standalone generator commands.

That is an important reality check for this page.

## Why generation still matters

Even with a smaller command set, generation is still valuable because it helps create Quantum-aligned structure.

The main benefits are:

- faster project setup
- less manual boilerplate
- template-based module structure
- consistent migration file creation
- automatic module config updates

## A practical way to use it

A normal flow can look like this:

1. generate a module
2. inspect the generated controllers, routes, middlewares, and views
3. edit the generated files for your feature
4. generate migrations as the database changes
5. run migrations with `php qt migration:migrate`

That is a much more accurate description of Quantum's current generation workflow than talking about broad generic scaffolding.

## Suggested next reading

These pages fit well with code generation:

- [The `qt` Command-Line Tool](qt-command-line-tool.md)
- [Console Commands](console-commands.md)
- [Modules Overview](../modules/overview.md)
- [Project Structure](../getting-started/project-structure.md)
