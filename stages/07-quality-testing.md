# Stage 7. Code quality and testing (ongoing)

Tests aren't about coverage, they're about the speed of confident change. A team afraid to touch its code loses money faster than a team that keeps tests. The goal of this stage isn't to learn xUnit, it's to understand which tests pay for themselves and where.

## Test types and where each one belongs

* Unit tests: pure logic, domain rules, algorithms. Run in milliseconds, no DB or network.
* Integration tests: combinations of multiple components, usually against real infrastructure via Testcontainers (Postgres, Redis, RabbitMQ in Docker).
* Contract tests (Pact, Verify): lock the contract between services and protect against breaking changes on the provider side.
* End-to-end: verify user scenarios as a whole. Expensive to maintain; keep a minimal smoke-check set.
* Testing pyramid vs testing trophy: for a .NET backend the trophy (a large share of integration tests via WebApplicationFactory) often pays off better than the classical pyramid.

## Tools

* Frameworks: xUnit as the de facto standard, NUnit where it historically stuck. MSTest is almost never seen in new projects.
* Assertions: FluentAssertions (watch out for the licensing change after version 8 — consider Shouldly or built-in xUnit assertions). AwesomeAssertions as a fork.
* Mocks: NSubstitute is preferable to Moq because of the 2024 licensing scandals and a cleaner API.
* Snapshots: Verify for checking complex objects and serialized payloads.
* Property-based: FsCheck and CsCheck for algorithms and parsers.
* Architecture tests: NetArchTest and ArchUnitNET to enforce rules like "the domain doesn't depend on infrastructure."
* Mutation testing: Stryker.NET, shows what tests actually catch, not just what they execute.

## Approaches and culture

* TDD where the requirements are fuzzy and you need design driven by tests. Not dogma, a tool.
* Arrange-Act-Assert as the base pattern; Given-When-Then for the BDD style.
* Test behavior, not implementation. If a test breaks on any refactor, it's testing the wrong thing.
* Excessive mocking is a sign of bad architecture. If you need to mock five dependencies in one test, the problem is the design of the class.
* Test data builders (Bogus, AutoFixture) for readable data setup.
* Coverage matters as a signal, not as a KPI. 80% coverage with tests without assertions is worse than 40% covering critical paths.

## Code quality

* Roslyn analyzers as the base: built-in .NET SDK rules, StyleCop.Analyzers, Meziantou.Analyzer.
* EditorConfig for unified formatting, .gitattributes for line endings.
* SonarQube or SonarCloud for tracking quality over time and detecting code smells.
* Code review culture: small PRs (up to 400 lines), description with context, a checklist for the reviewer. Conventional Commits for history.
* Pre-commit hooks via Husky.NET or lefthook: formatting, linting, fast tests.
* CI: test runs, static analysis, security scan (Snyk, Dependabot, GitHub Advanced Security) on every PR.

## Resources

* "Unit Testing: Principles, Practices, and Patterns" by Vladimir Khorikov, the leading book on tests in recent years.
* "The Art of Unit Testing" by Roy Osherove, third edition in C#.
* "Working Effectively with Legacy Code" by Michael Feathers, for those who work with a large existing codebase.
* Vladimir Khorikov's blog (enterprisecraftsmanship.com), especially the testing series.
* Documentation for Testcontainers (testcontainers.com) and FluentAssertions.

## Practice

1. Cover an existing service with integration tests through WebApplicationFactory and Testcontainers, including authorization and DB work.
2. Adopt Stryker.NET, find modules where mutations survive, fix the tests.
3. Write an architecture test that fails if the domain starts to depend on EF Core or ASP.NET Core.
4. Configure CI so the build fails when coverage of critical modules drops.

## Readiness signals for the next stage

* You can justify choosing between the trophy and the pyramid for a specific service.
* You've run Testcontainers in CI and know the typical traps (ports, cleanup, parallelism).
* You've used mutation testing and actually read the report, not just executed it.
* You've defended the code-review culture in front of a team that wants to "merge faster."

## Back to navigation

[All stages](README.md) | [Main README](../README.md)
