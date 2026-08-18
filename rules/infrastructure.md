# Infrastructure

Deployment and cloud-resource safety, separate from application code changes.

See [_format.md](_format.md) for the entry format.

---

### Treat production and infra changes as high risk
- **Rule:** Never destroy or modify production resources automatically. Don't touch deployment/infrastructure configuration unless the task requires it. Clearly flag any change that could affect production, data integrity, authentication, billing, or availability.
- **Why:** Infrastructure mistakes are often expensive, hard to reverse, and affect real users immediately.
- **Applies to:** any project with deployable infra (cloud resources, IaC, CI/CD)
