# Windows Autopatch — Automated Update Management

## Objective

This project configures Windows Autopatch to automate Windows quality updates, feature updates, Microsoft 365 Apps updates, and driver updates for the devices provisioned in [Microsoft Entra Joined/Cloud-Only Windows-11 Autopilot](../01-Entra-Joined-Cloud-Only-Windows11-Autopilot) and [Windows Autopilot Device Preparation](../03-Windows-Autopilot-Device-Preparation), replacing manually managed update policies with Microsoft-managed staged rollout groups.

### Skills Learned

- Autopatch prerequisites and readiness assessment
- Autopatch groups and deployment ring design (Test, First, Fast, Broad)
- Software update policy behavior once managed by Autopatch
- Reading the Autopatch device health and readiness reports

### Tools Used

- Windows Autopatch (within the Intune admin center — Tenant administration)
- Microsoft Entra ID security groups

## Steps

#### 1. Review Readiness and Enable Autopatch

Ran the built-in readiness assessment (Tenant administration → Windows Autopatch → Readiness) to confirm licensing, Entra join type, and update-related prerequisites before onboarding.

<img width="800" height="450" alt="image" src="docs/img/01-readiness-assessment.png" />

*Ref 1: Readiness check*

#### 2. Register Devices

Added `DG-Win11-Autopilot-Pilot` and `DG-Win11-DevicePrep-Pilot` to the Autopatch device registration scope, which automatically distributes their members across the deployment ring groups below.

<img width="800" height="450" alt="image" src="docs/img/02-device-registration.png" />

*Ref 2: Device registration*

#### 3. Configure Autopatch Groups (Deployment Rings)

| Ring Group | Purpose | Approx. device share |
|---|---|---|
| `DG-Win11-Autopatch-Ring-Test` | IT-only validation devices | 1–2 devices |
| `DG-Win11-Autopatch-Ring-First` | Early adopters, fast feedback | ~1% |
| `DG-Win11-Autopatch-Ring-Fast` | Broader validation before general rollout | ~9% |
| `DG-Win11-Autopatch-Ring-Broad` | Remaining fleet | ~90% |

<img width="800" height="450" alt="image" src="docs/img/03-deployment-rings.png" />

*Ref 3: Deployment rings*

#### 4. Review Auto-Generated Update Policies

Confirmed Autopatch automatically created and scoped Windows quality update, feature update, and driver update policies per ring group, so no manually created update policies were needed going forward.

<img width="800" height="450" alt="image" src="docs/img/04-update-policies.png" />

*Ref 4: Update policies*

#### 5. Monitor Device Health

Used the Autopatch Device Health report to track update compliance and flagged devices, and drilled into one flagged device to identify the blocking issue.

<img width="800" height="450" alt="image" src="docs/img/05-device-health.png" />

*Ref 5: Device health monitoring*

## About

Microsoft-managed, ring-based update rollout for the Windows 11 fleet built earlier in this portfolio, with no manually maintained update policies.
