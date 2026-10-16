# EffyKlean Hosting Decision — DigitalOcean Observation Period

**Decision date:** 16 October 2026  
**Status:** HU+DI agreed working decision  
**Scope:** Hosting-provider selection and post-launch evaluation

## Decision

EffyKlean will launch on **DigitalOcean** and use it as the hosting provider for an initial observation period of **at least 3 months, with 6 months preferred**, measured from go-live.

The goal is to evaluate DigitalOcean using real production experience before considering a provider migration.

## Operating approach

- Start with the lowest practical DigitalOcean configuration that satisfies EffyKlean's production, security, reliability, backup, and recovery requirements.
- Optimize and upgrade resources **within DigitalOcean** whenever evidence shows that additional capacity or resilience is needed. The observation period does not prohibit upgrades.
- Monitor actual performance, reliability, total cost, database health, operational effort, and recovery experience.
- After the observation period, consider another hosting provider **only if DigitalOcean does not meet EffyKlean's performance or cost expectations**, based on observed evidence.
- Reconsider earlier only if a serious security, reliability, compliance, or service-suitability issue makes remaining on DigitalOcean impractical.
- Any migration must be evidence-based and planned, with backup/restore, data integrity, cutover, and rollback considerations addressed.

## Boundaries

- This decision does not authorize provisioning resources, changing existing infrastructure, or incurring charges.
- The specific production configuration and estimated total cost must be reviewed and explicitly approved before resources are created or changed.
- DigitalOcean App Platform with Managed PostgreSQL remains the preferred direction, subject to confirming the smallest viable configuration and launch requirements.
- DigitalOcean Droplets remain a conditional alternative only if a demonstrated requirement justifies the additional server-management burden.
- AWS remains excluded under the existing project decision; GoDaddy remains a fallback to consider only if the preferred direction proves unsuitable.

## Review criteria

At the end of the observation period, review:

1. Application and checkout response times under actual usage.
2. Availability, error rates, and incident history.
3. Database performance, backup status, and demonstrated restore/recovery capability.
4. Total hosting and supporting-service costs.
5. Operational effort, deployment reliability, logs, monitoring, and support experience.
6. Whether DigitalOcean can continue meeting requirements through reasonable in-provider configuration changes.

## Next steps

1. Verify the current DigitalOcean account/project, existing resources, credits, and billing information.
2. Propose the lowest practical launch configuration and a transparent monthly cost estimate.
3. Define launch readiness, monitoring, backup, restore, and recovery checks.
4. Obtain explicit approval before provisioning or making chargeable changes.
5. Record the go-live date and schedule the 3-month review, with a 6-month review target if performance and cost remain satisfactory.

---

This document records the hosting-provider decision only. It does not claim that infrastructure has been provisioned, costs have been verified, or production readiness has been established.
