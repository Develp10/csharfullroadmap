# Contributing

Thanks for wanting to help make this roadmap better.

## Principles

- One PR per logical change. Big rewrites get discussed in an issue first.
- Tone: sober, applied, no marketing, no academic fluff.
- Add only vetted resources. In the PR description, briefly justify their value.
- Don't break the table of contents or section anchors. If you change a heading, update the TOC link.
- Typos and broken links: skip the issue, send the PR directly.

## How to submit a change

1. Fork the repository.
2. Create a branch: `git checkout -b fix/typo-stage-7` or `feat/add-resource-stage-11`.
3. Make the change, verify locally that markdown renders correctly.
4. Run `markdownlint` if you have it installed.
5. Open a PR against `main`, fill out the template.
6. Wait for review. Be ready to discuss.

## What will definitely be accepted

- Typo and grammar fixes.
- Updates to stale links and .NET versions.
- New vetted resources with justification.
- Wording refinements without changing meaning.
- New stages and sections agreed upon in an issue.
- Translations into other languages in separate `README.<lang>.md` files.

## What probably won't be accepted

- Ad links and affiliate courses without an explicit disclosure and real value.
- Removing existing sections without a replacement and reasoning.
- Holy wars about frameworks and editors.
- Stylistic changes for the sake of taste.
- Machine translation without proofreading by a native speaker.

## Writing style

- Short paragraphs, active voice, concrete verbs.
- Bulleted lists only for enumerations; for arguments, use prose.
- Code in ```csharp ... ``` blocks with syntax highlighting.
- Correct casing for technology names: ASP.NET Core, EF Core, PostgreSQL, Kubernetes.
- Numbers one through nine spelled out; from 10 onward, use digits.

## Code of Conduct

This project follows the [Contributor Covenant 2.1](CODE_OF_CONDUCT.md). Respect for participants is mandatory.
