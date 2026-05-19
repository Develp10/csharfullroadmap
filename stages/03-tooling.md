# Stage 3. Professional tooling

**Duration:** runs in parallel with Stages 1–2 and continues forever.

**Stage goal:** master the tools without which a strong team won't hire you. This isn't a separate course; it's the background you sink into as you grow.

## Git

Not just `add`, `commit`, `push`. You need to understand:

- Branching strategies: trunk-based development, GitHub Flow, Git Flow (the last one is almost always overkill).
- `rebase` vs `merge` — when and why.
- Cherry-pick, conflict resolution, `git reflog` for rescue.
- `git bisect` to find the commit that broke something.
- `git log -L`, `git blame -w -C -C -C` for archaeology.
- Working with large repos: shallow clone, sparse checkout, LFS.

Resource: the free [Pro Git book](https://git-scm.com/book/en/v2).

## Command line

- Bash or PowerShell at a confident-user level.
- Pipes, redirections, `grep`, `sed`, `awk`, `find`, `xargs`.
- Basic process handling: `ps`, `top`/`htop`, `kill`, `nohup`.
- SSH, scp, rsync, keys and agent.
- Aliases, scripts to automate daily tasks.

## Linux

Even if you work on Windows, production is almost always Linux.

- File system, permissions, owners and groups.
- Systemd: creating a service, logs through journalctl.
- Logging: `/var/log/`, rotation through logrotate.
- Networking: ifconfig/ip, netstat/ss, tcpdump for debugging.
- Package managers: apt, dnf, brew on Mac.

## Docker

- Images, layers, caching, multi-stage builds.
- Dockerfile best practices: minimize layers, security, size.
- docker-compose for local infrastructure.
- Network modes: bridge, host, overlay.
- Volumes vs bind mounts.
- Distroless and chiseled .NET images for production.

Book: **"Docker Deep Dive"** by Nigel Poulton.

## CI/CD

- **GitHub Actions** — the de facto standard for open source and many companies.
- **Azure DevOps Pipelines** — the corporate Microsoft environment.
- **GitLab CI** — if you use GitLab.

What your pipeline should be able to do:

- Build the project on every push.
- Run tests and publish results.
- Lint markdown, C#, YAML.
- Security scan: dependencies, secrets, containers.
- Build and publish artifacts (NuGet, Docker image).
- Deploy to staging automatically, to production by tag.

## Debugging and diagnostics

- **dotnet-dump** — capturing and analyzing memory dumps.
- **dotnet-counters** — monitoring counters (GC, ThreadPool, exceptions).
- **dotnet-trace** — collecting traces for analysis in PerfView or Speedscope.
- **dotnet-gcdump** — heap analysis without a full dump.
- **PerfView** — the flagship for performance analysis on Windows.
- **dotMemory, dotTrace** by JetBrains — UI alternatives.

## Benchmarking

**BenchmarkDotNet** — the standard for .NET microbenchmarks. It teaches discipline: don't trust intuition about performance.

```csharp
[MemoryDiagnoser]
[SimpleJob(RuntimeMoniker.Net80)]
public class Bench
{
    [Benchmark(Baseline = true)]
    public string Baseline() => "...";

    [Benchmark]
    public string Variant() => "...";
}
```

## Code analysis

- **EditorConfig** — unified code style across the team.
- **Roslyn analyzers** — static analysis at build time.
- **SonarQube, SonarCloud** — corporate quality gate.
- **NDepend** — deep architecture analysis (paid, expensive, but powerful).

## Dependency management

- Central Package Management via `Directory.Packages.props`.
- `dotnet outdated` for update checks.
- `dotnet list package --vulnerable` for vulnerability checks.
- Dependabot / Renovate for automated PRs.

## Readiness checklist

- [ ] I can run an interactive rebase to clean up commit history
- [ ] I understand the difference between `git merge --no-ff`, `--ff`, and `--squash`
- [ ] I use `git stash` and `git worktree` in everyday work
- [ ] I work confidently in a terminal without visual file managers
- [ ] I can write a working Dockerfile for an ASP.NET Core app
- [ ] I've set up GitHub Actions for my pet project
- [ ] I've taken a dotnet-dump and analyzed it
- [ ] I've run at least one benchmark through BenchmarkDotNet
- [ ] I use `.editorconfig` in all my projects
- [ ] I understand what a quality gate is and why I need one

## Navigation

[← Stage 2](02-platform.md) | [All stages](README.md) | [Main README](../README.md)
