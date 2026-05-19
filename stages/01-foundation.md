# Stage 1. Language and platform foundations

**Duration:** 1–2 months full-time or 3 months in parallel with work or studies.

**Stage goal:** confidently write, read, and debug medium-sized C# code. Understand the type system and basic constructs without checking the docs every five minutes.

## Environment

Install the current .NET SDK (LTS — .NET 8, latest release — .NET 9). Pick an IDE:

- **JetBrains Rider** — the best balance for most people, especially on Mac or Linux.
- **Visual Studio 2022** — the standard in corporate Windows development.
- **VS Code + C# Dev Kit** — for lightweight tasks and remote work via Codespaces.

Also:

- Git (the Pro Git book as your reference).
- A terminal (Windows Terminal, iTerm2, or the IDE's built-in one).
- A GitHub account with an SSH key configured.

## What to master

### Syntax

- Value and reference types, nullable reference types, default values.
- Pattern matching: `is`, `switch` statements, switch expressions, property patterns.
- Records, init-only properties, with-expressions.
- String interpolation, raw string literals, UTF-8 strings.
- Control flow, methods, overloads, optional and named arguments.

### OOP

- Encapsulation, inheritance, polymorphism.
- Interfaces (including default interface methods).
- Abstract classes, sealed classes, partial.
- Composition vs inheritance — knowing when to pick which.
- Generics, type constraints, covariance and contravariance.

### Functional elements

- Delegates, events, lambda expressions.
- Closures and their pitfalls (variable capture).
- LINQ to Objects: `Where`, `Select`, `GroupBy`, `Aggregate`, `Any`, `All`.
- Deferred execution and materialization — why it matters for performance.

### Exceptions

- The .NET exception hierarchy.
- when-filters in catch blocks.
- finally, correct rethrowing (`throw` vs `throw ex`).
- When not to catch exceptions.

### Collections

- `List<T>`, `Dictionary<TKey, TValue>`, `HashSet<T>`, `Queue<T>`, `Stack<T>`.
- `ImmutableArray`, `ImmutableList`, `ImmutableDictionary`.
- When to use an array, a list, or a dictionary.

## Resources

### Books

- **Jon Skeet, "C# in Depth"** — the mandatory minimum. Especially the chapters on generics, delegates, async.
- **Joseph Albahari, "C# 12 in a Nutshell"** — a reference for the whole language.

### Documentation

- [Microsoft Learn for C#](https://learn.microsoft.com/dotnet/csharp/)
- [.NET API Browser](https://learn.microsoft.com/dotnet/api/)
- [C# Language Reference](https://learn.microsoft.com/dotnet/csharp/language-reference/)

### Videos

- Nick Chapsas on YouTube — short, practical breakdowns.
- Tim Corey — for beginners, presented from scratch.
- IAmTimCorey, ZoranHorvat — advanced OOP.

### Courses

- [C# Fundamentals](https://www.pluralsight.com/courses/csharp-fundamentals-dev) by Scott Allen on Pluralsight.
- The free [.NET modules on Microsoft Learn](https://learn.microsoft.com/training/dotnet/).

## Practice

### Minimum

1. Solve 50 problems on [Codewars](https://www.codewars.com/) from 8 kyu to 5 kyu in C#.
2. Solve 50 Easy-level problems on [LeetCode](https://leetcode.com/) in C#.

### Pet project

A text-based task manager (CLI) with the following capabilities:

- Add, edit, delete, search tasks.
- Categories, tags, priorities, deadlines.
- JSON file persistence via `System.Text.Json`.
- Commands via command-line arguments (`System.CommandLine`).
- Colored output via `Spectre.Console`.
- Unit tests for the core business logic.

**Project readiness checklist:**

- [ ] README with run instructions
- [ ] `.gitignore` for C# projects
- [ ] At least 20 commits with meaningful messages
- [ ] Logical project split (Domain, App, CLI, Tests)
- [ ] 30+ passing tests
- [ ] An `.editorconfig` for a unified style

## Readiness checklist for Stage 2

- [ ] I can write a class with a constructor, properties, and methods without hints
- [ ] I understand the difference between `class` and `struct` and can explain when to use which
- [ ] I know what a generic constraint is and can apply one
- [ ] I use LINQ for typical tasks (filtering, grouping, aggregation)
- [ ] I understand closures and see the trap of capturing a variable in a loop
- [ ] I can write a custom exception and rethrow it correctly
- [ ] I use records for immutable data
- [ ] I understand pattern matching and apply switch expressions
- [ ] I don't use `throw ex` (I know why)
- [ ] I don't confuse value and reference types in typical scenarios

## Navigation

⏮ [All stages](README.md) | [Main README](../README.md) | [Stage 2 →](02-platform.md)
