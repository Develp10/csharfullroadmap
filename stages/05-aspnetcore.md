# Stage 5. ASP.NET Core and web development (2–3 months)

ASP.NET Core is the workhorse of most .NET teams. The goal of this stage isn't just to stand up a Hello World, it's to understand what happens in the pipeline, how authentication works in real products, and how to ship a service into operation without surprises.

## What to master

* Kestrel as the HTTP server, reverse proxies (Nginx, YARP), HTTP/2 and HTTP/3, gRPC transport.
* The middleware pipeline: order matters; understanding Use, Run, Map, custom middleware for logging, correlation, error handling.
* The DI container: lifetimes (Singleton, Scoped, Transient), captive dependency, registration by interface, the decorator pattern via Scrutor.
* Configuration: appsettings, environment variables, secret stores (Azure Key Vault, AWS Secrets Manager, HashiCorp Vault). The Options pattern, `IOptionsMonitor` for hot reload.
* Minimal APIs vs controllers. Minimal APIs win on performance and readability for small services; controllers are more convenient in large APIs with filters and complex routing.
* Model binding, validation (FluentValidation or DataAnnotations), mapping (Mapster, manual mapping). AutoMapper is picked less often in new projects because of licensing changes and hidden magic.

## Authentication and authorization

* JWT tokens: structure, signing, validation, refresh tokens, secure storage on the client.
* OAuth 2.0 and OpenID Connect: grants, flows, scopes. Identity providers: Auth0, Keycloak, IdentityServer (Duende), Azure AD B2C.
* ASP.NET Core Identity for a self-hosted user system, when an external provider would be overkill.
* Policy-based vs role-based authorization, claims, requirement handlers.
* Protection against common attacks: CSRF, XSS, open redirects, IDOR. ASP.NET Core ships with built-in mechanisms; you need to understand when they apply and when they don't.

## Observability and operations

* Structured logging through `ILogger` and Serilog, request correlation via TraceId.
* OpenTelemetry: tracing, metrics, exporters to Jaeger, Tempo, Prometheus, Grafana. This is the industry standard, not an option.
* Health checks (liveness, readiness), graceful shutdown, hosted services, BackgroundService.
* ProblemDetails for uniform API errors, idempotency of critical operations, API versioning (URL, header, media type).
* Swagger/OpenAPI and client generation (NSwag, Kiota).

## Additional technologies

* gRPC for internal service-to-service communication, contract-first approach via `.proto`.
* SignalR for real-time scenarios: chats, dashboards, notifications. Understand scaling limits and the backplane (Redis).
* GraphQL via HotChocolate when the client has complex data-fetching requirements. Downsides: caching and rate-limiting complexity.
* Background jobs: Hangfire, Quartz.NET, or native HostedService for simple scenarios.

## Resources

* "ASP.NET Core in Action" by Andrew Lock, the current edition for the latest LTS.
* Andrew Lock's blog (andrewlock.net), deep dives into framework internals.
* Microsoft's ASP.NET Core documentation, especially the Security and Performance sections.
* Nick Chapsas' YouTube channel for practical feature breakdowns.
* David Fowler's GitHub blog (davidfowl/AspNetCoreDiagnosticScenarios) is required reading.

## Practice

Build a full-fledged API for a task service:

1. Authorization through JWT with refresh tokens and roles.
2. Persistence through EF Core, migrations, repositories or direct DbContext use.
3. Validation through FluentValidation, manual mapping.
4. Structured logs in Serilog, trace export to Jaeger.
5. Health checks, Dockerfile, deployment to the cloud (Azure App Service, AWS ECS, or Kubernetes).
6. CI/CD through GitHub Actions with test and lint runs.

## Readiness signals for the next stage

* You understand why middleware order matters and can write a custom one on the spot.
* You can explain the difference between Scoped and Singleton without prompts and give a captive dependency example.
* You've configured OpenTelemetry in a project that shipped to production.
* You can design an API so that a repeated request doesn't create a duplicate payment.

## Back to navigation

[All stages](README.md) | [Main README](../README.md)
