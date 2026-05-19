# Stage 8. Cloud and operations (1–2 months)

In 2026, writing a backend without understanding cloud and operations is writing half the job. The Middle vs Senior gap often shows up exactly here: not only can you implement a feature, you also understand what will happen to it in production, under load, when an availability zone fails.

## Cloud platforms

* Azure is closer to the .NET stack through integrations (App Service, Functions, Service Bus, Cosmos DB, Application Insights). The AZ-204 certification gives a systematic view.
* AWS offers more jobs on the global market. Minimum: EC2, ECS/EKS, RDS, S3, SQS, SNS, Lambda, IAM. The Developer Associate certification.
* GCP shows up less often in .NET roles but appears on data teams.
* The cloud isn't a panacea: vendor lock, surprise bills, cold-start effects in serverless. Understand when picking a managed service is cheaper and simpler, and when self-hosting wins.

## Containers and orchestration

* Docker: multi-stage builds, minimal base images (chiseled containers for .NET 8+, distroless), image security (Trivy, Grype).
* Kubernetes basics: Pod, Deployment, Service, Ingress, ConfigMap, Secret, HorizontalPodAutoscaler.
* Helm and Kustomize for manifest management. Argo CD or Flux for GitOps.
* Service mesh (Istio, Linkerd) at an overview level, enough to understand which problem it solves.
* Alternatives to Kubernetes for small projects: Azure Container Apps, AWS ECS Fargate, Google Cloud Run. Often simpler and cheaper.

## Infrastructure as Code

* Terraform as the industry standard, OpenTofu as a fork after the license change.
* Bicep in the Azure stack as a more convenient alternative to ARM templates.
* Pulumi for those who want to describe infrastructure in C#.
* The immutable infrastructure principle: environments are recreated, not edited by hand.
* State management: remote state, locking, separation by environment and service.

## Production observability

* Metrics through Prometheus and Grafana, or cloud equivalents (Application Insights, CloudWatch, Google Cloud Monitoring).
* Tracing through OpenTelemetry, export to Jaeger, Tempo, Honeycomb, Datadog.
* Logs: structured, correlated by TraceId. Loki, ELK, or cloud services.
* SLI, SLO, error budget as a way to negotiate quality with product. The "Site Reliability Engineering" book from Google is the foundation.
* Alerting based on symptoms (the user is suffering), not causes (CPU 80%). Avoid alert fatigue.

## CI/CD

* GitHub Actions, GitLab CI, Azure DevOps Pipelines. The principles are the same, the syntax differs.
* Trunk-based development vs Git Flow. For most teams, trunk-based with feature flags is simpler and faster.
* Deployment strategies: blue-green, canary, rolling. When to use which.
* Feature flags via LaunchDarkly, Unleash, Flagsmith, or a homegrown solution. They decouple deploy from release.
* Secrets management: GitHub Secrets, Azure Key Vault, HashiCorp Vault, AWS Secrets Manager. Never commit secrets, even to a private repository.

## Operations security

* OWASP Top 10 and OWASP API Top 10 as a checklist.
* Protection against common attacks: SQL injection (parameterized queries), SSRF, XXE, deserialization, IDOR.
* Dependency management: Dependabot, Renovate, Snyk. SBOM (CycloneDX, SPDX) for supply chain transparency.
* Principle of least privilege: IAM roles, managed identities, RBAC in Kubernetes.
* Network security: private endpoints, VPC peering, WAF.

## Resources

* "Site Reliability Engineering" and "The Site Reliability Workbook" by Google, free online.
* "Designing Distributed Systems" by Brendan Burns.
* "Kubernetes Up and Running" by Brendan Burns et al.
* "Terraform: Up and Running" by Yevgeniy Brikman.
* The TechWorld with Nana YouTube channel for practical introductions to DevOps.
* Cloud-provider docs and the CNCF (cncf.io).

## Practice

1. Deploy a full-fledged .NET service to Kubernetes (managed: AKS, EKS, GKE) with Helm charts, Ingress, secrets from Vault, metrics in Prometheus.
2. Write a Terraform module for a typical stack (DB, queue, service, load balancer) with dev/staging/prod separation.
3. Set up a full CI/CD pipeline: tests, security scan, build image, deploy to staging, manual approval for prod.
4. Define SLI and SLO for your service, configure alerting on their breaches.

## Readiness signals for the next stage

* You've stood up and operated a Kubernetes cluster, not just run `helm install`.
* You can explain why a CPU alert isn't needed and a P99 latency alert is.
* You've written Terraform code that recreates an environment from scratch without manual steps.
* You've investigated a production incident through traces and metrics and written a blameless postmortem.

## Back to navigation

[All stages](README.md) | [Main README](../README.md)
