# TECHNOLOGY IMPLEMENTATION SPECIFICATION TEMPLATE
## Blank Production Application Platform — Version 0.02.0

# 1. Purpose

Document 06 is the authoritative project-specific technology decision record. Fill only decisions that constrain implementation now; use `DEFERRED` with a trigger instead of speculative precision. Generated project artifacts derive from the completed copy.

# 2. Decision Record Rules

Each decision uses concise fields. `Status`: `PROPOSED`, `APPROVED`, `DEFERRED`, `NOT APPLICABLE`, `REJECTED`. Mature mainstream technology is preferred. Record ADR only for material architecture/security/lock-in decisions.

# 3. Timing

Use one of: `FOUNDATION`, `BEFORE CAPABILITY`, `BEFORE PRODUCTION`, `DEFER UNTIL TRIGGERED`. Resolve the smallest set needed to proceed safely.

# 4. Canonical Selection Rules

- satisfy Documents 01/03/04 first;
- prefer existing toolbox/framework primitives over wrappers;
- new reusable primitive requires Toolbox Gap user decision;
- separate mechanisms from delivery obligations;
- minimize dependencies/operational complexity;
- choose the cheapest mature option meeting hard requirements;
- do not fabricate scale, RPO/RTO, residency or legal precision.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.

# 5. Executive Technology Summary

**Classification:** GENERAL



```text
Primary Language(s):
Runtime:
Backend Framework:
Frontend Framework:
Database:
ORM / Data Access:
Migration Tool:
Queue / Worker:
Object Storage:
Authentication:
Authorization:
Secrets Store:
Hosting:
CI/CD:
Status:
```

# 6. External Constraints

**Classification:** MANDATORY



```text
Deployment Owner:
Hosting Constraints:
Cloud Preference:
Data Residency:
Expected User Scale:
Expected Tenant Scale:
Availability Expectation:
Recovery Expectation:
Budget Range:
Operating Skill Level:
Supported Browsers:
Self-Hosting Requirement:
Commercial-Service Constraints:
Licensing Constraints:
AI Cost Priority:
Portability Priority:
Vendor Lock-In Tolerance:
Status:
```

# 7. Programming Language and Type Policy

**Classification:** MANDATORY



```text
Backend Language:
Frontend Language:
Version Policy:
Strictness / Type Policy:
Other Approved Languages:
Additional-Language Approval Rule:
Status:
```

# 8. Runtime

**Classification:** MANDATORY



```text
Runtime:
Version Policy:
Support / EOL Policy:
Runtime Pinning Mechanism:
Status:
```

# 9. Backend Framework

**Classification:** MANDATORY



```text
Framework:
Version Policy:
Server Model:
Middleware / Request Pipeline:
Status:
```

# 10. Frontend Framework and Rendering

**Classification:** MANDATORY



```text
Framework:
Rendering Model:
Client / Server Boundary:
Routing Model:
Status:
```

# 11. UI Styling and Components

**Classification:** MANDATORY



```text
Styling Strategy:
Component Library:
Design Tokens:
Accessibility Baseline:
New UI Primitive Policy:
Status:
```

# 12. Repository and Package Management

**Classification:** MANDATORY



```text
Repository Model:
Package Manager:
Lockfile Required:
Workspace Layout:
Dependency Update Policy:
Status:
```

# 13. Deployment Shape

**Classification:** MANDATORY



```text
Deployment Shape:
Service Split Trigger:
Shared Library Policy:
Status:
```

# 14. API Protocol and Schema

**Classification:** MANDATORY



```text
Primary API Style:
Serialization:
Schema Standard:
Versioning Strategy:
Status:
```

# 15. API Request Semantics

**Classification:** MANDATORY



```text
Validation Mechanism:
Error Format:
Pagination:
Filtering:
Sorting:
Request Limits:
Idempotency Mechanism:
Concurrency Mechanism:
Status:
```

# 16. Database Engine

**Classification:** MANDATORY



```text
Database:
Version Policy:
Hosting Model:
Connection / Pooling Strategy:
Status:
```

# 17. Persistence / Data Access

**Classification:** MANDATORY



```text
ORM / Query Layer:
Repository Pattern:
Transaction API:
Tenant Scoping Mechanism:
Raw SQL Policy:
Error Translation:
Query Observability:
Status:
```

# 18. Identifiers and Naming

**Classification:** MANDATORY



```text
Primary Identifier Type:
Tenant Identifier Type:
Database Naming Convention:
Public Identifier Policy:
Status:
```

# 19. Schema Migrations

**Classification:** MANDATORY



```text
Migration Tool:
Migration Ownership:
Production Execution:
Locking:
Expand / Migrate / Contract Policy:
Rollback Policy:
Status:
```

# 20. Transactions and Concurrency

**Classification:** MANDATORY



```text
Default Isolation:
Transaction Boundary Policy:
Optimistic Concurrency Token:
Locking Policy:
Status:
```

# 21. Tenant Isolation

**Classification:** MANDATORY



```text
Tenant Context Source:
Application Query Scoping:
Database RLS:
RLS Context Mechanism:
Cross-Tenant Test Strategy:
Status:
```

# 22. Organisation Hierarchy

**Classification:** MANDATORY



```text
Hierarchy Representation:
Membership Representation:
Scope Inheritance:
Status:
```

# 23. Authorization

**Classification:** MANDATORY



```text
Authorization Engine:
Permission Registry:
RBAC Representation:
ABAC / Context Representation:
Default Deny Mechanism:
Caching Policy:
Status:
```

# 24. Authentication Platform

**Classification:** MANDATORY



```text
Provider / Library:
Local Password Support:
Passkey / WebAuthn Support:
MFA Support:
Account Recovery:
Email Verification:
Phone Verification:
Status:
```

# 25. Federation and Account Linking

**Classification:** CONDITIONAL



```text
OIDC:
SAML:
External Claim Mapping:
Account Linking Policy:
Status:
```

# 26. Session Management

**Classification:** MANDATORY



```text
Session Model:
Session Store:
Cookie / Token Policy:
Rotation:
Revocation:
Idle Timeout Policy:
Absolute Lifetime Policy:
Status:
```

# 27. Elevation / Impersonation / Break-Glass

**Classification:** MANDATORY



```text
Elevation Mechanism:
Recent Auth Requirement:
MFA Requirement:
Impersonation Model:
Break-Glass Policy:
True / Effective Actor Audit:
Status:
```

# 28. Secrets Management

**Classification:** MANDATORY



```text
Secrets Store:
Injection Mechanism:
Rotation Policy:
Local Development Secrets:
Secret Reference Pattern:
Audit / Access Policy:
Status:
```

# 29. Cryptographic Key Management

**Classification:** MANDATORY



```text
KMS / Key Store:
Signing Key Storage:
Encryption Key Storage:
Rotation Policy:
Recovery Policy:
Status:
```

# 30. TLS, Edge and Reverse Proxy

**Classification:** MANDATORY



```text
TLS Termination:
Reverse Proxy / Edge:
Trusted Forwarded Headers:
HSTS / Security Headers:
Origin Exposure Policy:
Status:
```

# 31. Application Security and Abuse Protection

**Classification:** MANDATORY



```text
CORS:
CSRF:
CSP:
Rate Limiting:
Login / Recovery Abuse Controls:
Request Size Limits:
SSRF Strategy:
Bot / CAPTCHA Trigger:
Status:
```

# 32. Audit

**Classification:** MANDATORY



```text
Primary Audit Store:
Append-Only Enforcement:
Audit Write Strategy:
Event Schema:
PII Minimisation:
Immutability / WORM Trigger:
Retention / Legal Hold Integration:
Status:
```

# 33. Outbox and Events

**Classification:** MANDATORY



```text
Outbox Storage:
Publisher:
Event Envelope:
Delivery Semantics:
Consumer Idempotency:
Schema Versioning:
Status:
```

# 34. Queue and Workers

**Classification:** MANDATORY



```text
Queue:
Worker Runtime:
Delivery Semantics:
Retry Policy:
DLQ:
Job Timeout:
Graceful Shutdown:
Operational Inspection:
Status:
```

# 35. Scheduling

**Classification:** CONDITIONAL



```text
Scheduler:
Leader / Duplication Control:
Missed-Run Policy:
Timezone Policy:
Status:
```

# 36. Notifications

**Classification:** CONDITIONAL



```text
Email Provider:
SMS Provider:
Push Provider:
Provider Abstraction:
Templates:
Retry / Deduplication:
Development Sink:
Status:
```

# 37. Object Storage

**Classification:** CONDITIONAL



```text
Object Store:
Tenant Segmentation:
Presigned URL Strategy:
Upload Limits:
Malware Scanner:
Image / File Processing Isolation:
CDN:
Status:
```

# 38. Configuration

**Classification:** MANDATORY



```text
Setting Definitions Storage:
Setting Values Storage:
Scope / Precedence:
Validation:
Secret Settings Policy:
Audit:
Status:
```

# 39. Feature Flags

**Classification:** MANDATORY



```text
Feature Flag System:
Targeting:
Kill Switches:
Audit:
Safe Default:
Status:
```

# 40. Time and Timezone

**Classification:** MANDATORY



```text
Time Library:
Instant Representation:
Timezone Source:
Clock Abstraction:
Fake Clock:
Status:
```

# 41. Internationalisation and Text

**Classification:** MANDATORY



```text
I18n Library:
Locale Source:
Fallback Locale:
Unicode Encoding:
Translation Resource Strategy:
Status:
```

# 42. Money and Decimal

**Classification:** MANDATORY



```text
Decimal Type:
Money Type:
Currency Source:
Rounding Policy:
Precision / Scale Policy:
Currency Mismatch Policy:
Status:
```

# 43. Privacy / Data Lifecycle Mechanism

**Classification:** CONDITIONAL



```text
Policy Acceptance:
Data Export:
Deletion / Anonymisation:
Retention Engine:
Legal Hold Mechanism:
Data Classification:
Status:
```

# 44. Logging

**Classification:** MANDATORY



```text
Logging Library:
Format:
Correlation:
Redaction:
PII Policy:
Retention Destination:
Status:
```

# 45. Metrics / Tracing / Error Tracking

**Classification:** MANDATORY



```text
Metrics Library / Backend:
Tracing Library / Backend:
Error Tracking:
Sampling Policy:
Status:
```

# 46. Health / Readiness

**Classification:** MANDATORY



```text
Liveness Endpoint:
Readiness Endpoint:
Dependency Registry:
Degraded Dependency Policy:
Public Detail Policy:
Status:
```

# 47. Maintenance / Graceful Degradation

**Classification:** MANDATORY



```text
Maintenance State Store:
Read-Only Mode:
API Behaviour:
Job Behaviour:
Admin Recovery Access:
Connection Draining:
Status:
```

# 48. Platform Administration

**Classification:** MANDATORY



```text
Admin UI / API Framework:
Permission Model:
Elevation Policy:
Audit:
Environment Marking:
Status:
```

# 49. Platform Data Inspector

**Classification:** MANDATORY



```text
Implementation Approach:
Development Capabilities:
Staging Restrictions:
Production Restrictions:
Sensitive Field Masking:
Mutation Permission:
Status:
```

# 50. Data Inspector Query Safety

**Classification:** MANDATORY



```text
Direct SQL Policy:
Statement Timeout:
Row Limit:
Read / Write Separation:
Query Audit:
Production Enablement Approval:
Status:
```

# 51. Infrastructure Hosting

**Classification:** MANDATORY



```text
Provider:
Primary Region:
Secondary Region:
Compute Service:
Container Runtime:
Base Image:
Status:
```

# 52. Networking / DNS

**Classification:** MANDATORY



```text
Network Model:
Ingress:
Egress Restrictions:
DNS Provider:
Certificate Management:
Status:
```

# 53. High Availability and Scaling

**Classification:** MANDATORY



```text
HA Strategy:
Horizontal Scaling:
Stateful Constraints:
Autoscaling:
Resource Limits:
Status:
```

# 54. Multi-Region

**Classification:** OPTIONAL



```text
Active / Passive:
Active / Active:
Replication Model:
Failover Authority:
Trigger for Adoption:
Status:
```

# 55. Database Hosting and Recovery Features

**Classification:** MANDATORY



```text
Managed Database Service:
Encryption At Rest:
Automated Backups:
Point-in-Time Recovery:
Failover:
Maintenance Window:
Status:
```

# 56. Backup / Restore / DR Obligation

**Classification:** MANDATORY



```text
Backup Mechanism:
Retention:
Restore Procedure:
Restore Test Cadence:
RPO:
RTO:
Recovery Credential Strategy:
Evidence Location:
Status:
```

# 57. Rate Limit / Abuse Delivery Obligation

**Classification:** MANDATORY



```text
Public Endpoint Assessment:
Authenticated Endpoint Assessment:
Admin / Expensive Operation Assessment:
Limit Policy:
Failure Policy:
Evidence Location:
Status:
```

# 58. Data Lifecycle Delivery Obligation

**Classification:** MANDATORY



```text
Data Class Inventory:
Retention Policy:
Deletion / Anonymisation Policy:
Export Policy:
Backup / Archive Treatment:
Legal Hold Applicability:
Evidence Location:
Status:
```

# 59. Operational Resilience Obligation

**Classification:** MANDATORY



```text
Critical Dependency Inventory:
Timeout Policy:
Retry Policy:
Idempotency Policy:
Degradation / Circuit Breaker Policy:
Failure Containment Evidence:
Status:
```

# 60. CI Platform

**Classification:** MANDATORY



```text
CI Provider:
Required Checks:
Cache Policy:
Secret / Permission Model:
Status:
```

# 61. CD and Deployment

**Classification:** MANDATORY



```text
Deployment Tool:
Promotion Model:
Migration Coordination:
Readiness Gate:
Rollback / Recovery:
Production Approval:
Status:
```

# 62. Infrastructure as Code

**Classification:** MANDATORY



```text
IaC Tool:
State Storage:
Review / Apply Policy:
Drift Detection:
Status:
```

# 63. Source Control / Review

**Classification:** MANDATORY



```text
Repository Host:
Default Branch:
Protected Branches:
PR Requirement:
Required Review:
Code Owners:
Status:
```

# 64. Local Development

**Classification:** MANDATORY



```text
Local Runtime:
One-Command Startup:
Local Database:
Fake Providers:
Offline Capability:
Status:
```

# 65. Test / Staging / Production Environments

**Classification:** MANDATORY



```text
Environment Identity Mechanism:
Test Isolation:
Staging Restrictions:
Production Restrictions:
Production Data Masking:
Status:
```

# 66. Test Frameworks

**Classification:** MANDATORY



```text
Unit Test Framework:
Integration Test Framework:
E2E Framework:
Contract Test Framework:
Security Test Tooling:
Architecture Test Mechanism:
Status:
```

# 67. Test Data and Scenarios

**Classification:** MANDATORY



```text
Factory / Fixture Strategy:
Deterministic Seed:
Named Scenarios:
Reset / Clear:
Protected State Enforcement:
Fake Clock / Random:
Status:
```

# 68. Test Impact and Flaky Policy

**Classification:** MANDATORY



```text
Affected-Test Selection:
Full-Suite Fallback:
Selected-Test Rationale:
Flaky Test Policy:
Status:
```

# 69. Supply Chain Security

**Classification:** MANDATORY



```text
Dependency Inventory:
Vulnerability Scanning:
Secret Scanning:
Licence Review:
SBOM:
Artifact Signing / Provenance:
Status:
```

# 70. Observability Operations

**Classification:** MANDATORY



```text
Dashboard Strategy:
Alerting:
On-Call / Incident Path:
Log / Metric Retention:
Status:
```

# 71. Performance and Capacity Obligation

**Classification:** MANDATORY



```text
Initial Scale Assumption:
Performance Targets:
Load Test Trigger:
Capacity Review Trigger:
Resource / Cost Guardrails:
Status:
```

# 72. AI Engineering Environment

**Classification:** MANDATORY



```text
Primary AI Coding Environment:
Superpowers Mode:
Native Blank Fallback:
Model Selection Policy:
Context Strategy:
Delegation Policy:
Cost Tracking:
Status:
```

# 73. Toolbox and Mature Contract Governance

**Classification:** MANDATORY



```text
Toolbox Registry Location:
Mature Contract Marker:
Search Procedure Before New Primitive:
Toolbox Gap User Approval:
External Solution Review:
Contract Change Approval:
Status:
```

# 74. Agent Repository Artifacts

**Classification:** MANDATORY



```text
AGENTS Path:
Context Map Path:
Capability Registry Path:
Toolbox Registry Path:
Technology Profile Path:
Commands Path:
Environment Matrix Path:
Status:
```

# 75. Documentation / ADRs

**Classification:** MANDATORY



```text
Canonical Docs Path:
ADR Path:
ADR Trigger:
Runbooks Path:
Documentation Update Trigger:
Status:
```

# 76. Supported Deployment Scope

**Classification:** MANDATORY



```text
Supported Deployment Models:
Explicitly Unsupported Models:
Portability Boundary:
Vendor Lock-In Acceptance:
Status:
```

# 77. Optional Distributed Cache

**Classification:** OPTIONAL



```text
Approved Now:
Technology:
Trigger:
Invalidation Strategy:
Status:
```

# 78. Optional Dedicated Search

**Classification:** OPTIONAL



```text
Approved Now:
Technology:
Trigger:
Tenant / Security Model:
Status:
```

# 79. Optional Analytics / Reporting

**Classification:** OPTIONAL



```text
Approved Now:
Technology:
Trigger:
Security Boundary:
Status:
```

# 80. Optional Enterprise Complexity

**Classification:** OPTIONAL



```text
Kubernetes:
Service Mesh:
API Gateway:
CQRS / Read Model:
Distributed Locks:
Chaos Engineering:
Trigger / Rationale:
Status:
```

# 81. Technology Completion Review

**Classification:** MANDATORY



```text
Approved Decisions Complete:
Deferred Decisions Have Trigger:
Not Applicable Has Rationale:
Blocking Unknowns:
Security Review Complete:
Toolbox Gaps Resolved:
Status:
```

# 82. Domain-Entry Readiness

**Classification:** MANDATORY



```text
Clean Build / Start:
Fresh Migration:
Auth / Revocation:
Tenant / Cross-Tenant Denial:
Default-Deny Authz:
Audit / Config / Jobs:
Health / Logging:
Test Data / Protected State:
Admin / Data Inspector Controls:
Backup Mechanism:
Agent / Toolbox Artifacts Current:
Status:
```

# Mandatory Decision Principle

A decision is resolved when it is `APPROVED`, `NOT APPLICABLE` with rationale, or `DEFERRED` with a concrete trigger and the deferral cannot invalidate current work. Do not force production-only precision into the first coding iteration.

# Completion Output

The completed project copy of Document 06 is authoritative for implementation technology. Regenerate derived `PROJECT_*` files after material changes.
