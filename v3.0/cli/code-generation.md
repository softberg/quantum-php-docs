# Code Generation

One of the most practical parts of a framework CLI is code generation.

In the Quantum PHP Framework, generation commands help you create framework-aligned structure faster instead of building every file and folder manually.

## Why code generation matters

When developers are new to a framework, they often do not just need to create code.
They need to create code in the right place and in the right shape.

That is where generation commands help.

They reduce uncertainty by making it easier to:

- follow framework conventions
- create repeatable structure
- avoid boilerplate mistakes
- move faster when building new features

## Core idea

Think of code generation as scaffolding.

You are not asking the CLI to build the entire application for you.
You are asking it to create the correct starting structure so you can focus on the actual feature logic.

## What generation usually helps create

In a Quantum project, generation is especially useful around module-based architecture.

Depending on the command, it may help create things like:

- modules
- controllers
- middlewares
- supporting framework directories and files

This keeps your project layout consistent with how Quantum expects applications to grow.

## Why this is useful in real projects

Manual file creation sounds simple in a tiny project.
But as the project grows, consistency matters more.

Generated structure helps teams keep:

- naming predictable
- folders consistent
- shared conventions easier to follow

That is especially important when multiple modules are involved.

## When to use generation commands

You should reach for generation commands when:

- starting a new module
- adding a new framework-level component
- learning the framework's preferred structure
- trying to avoid repetitive setup work

The biggest benefit is not speed alone. It is confidence.

If the framework generates the structure, you know you are starting from a valid baseline.

## Code generation and architecture

Good CLI generation does more than save keystrokes.
It reinforces the framework's architecture.

In Quantum, that matters because modules, middleware, and controller structure are part of how applications are organized.

So generation commands help teach architecture while also creating files.

## What generation does not replace

It is still important to understand the framework concepts behind the generated files.

The CLI can create:

- the file
- the folder
- the starter structure

But you still need to understand:

- when to use a controller
- when middleware belongs on a route
- how a module fits into the project
- what the generated code is supposed to do

So generation should support learning, not replace it.

## A practical rule

Use generation commands when they help you stay aligned with framework conventions.

Do not treat generated code as magic.
Read what the CLI created and understand why it belongs there.

That is the fastest path to becoming comfortable with the framework.

## Suggested next reading

If you are learning Quantum through hands-on building, these pages fit well with code generation:

- [Modules Overview](../modules/overview.md)
- [Controllers](../core-concepts/controllers.md)
- [Middleware](../core-concepts/middleware.md)
- [Project Structure](../getting-started/project-structure.md)
