# Cloud Security Risk Assessment on Oracle Cloud Infrastructure (OCI)

## Overview

This project simulates a real-world cloud security assessment on **Oracle Cloud Infrastructure (OCI)**. I built a small cloud environment (network, compute, storage, IAM), deliberately introduced common real-world misconfigurations, detected them using OCI's native security tooling, scored each finding against the **CIS OCI Foundations Benchmark**, and applied remediations — the full lifecycle a Cloud Security / GRC analyst would run.

**Goal:** demonstrate hands-on understanding of cloud identity, networking, and risk assessment methodology — not just theory.

## Why this project

Applying for a cybersecurity internship, I wanted a project that went beyond typical on-prem/AD pentesting (which I already have experience in — see my [Active Directory pentest work](#)) and demonstrated cloud security fundamentals: IAM, shared responsibility model, and compliance frameworks.

## Architecture

```
                    Internet
                        │
                 [Internet Gateway]
                        │
                 ┌──────┴──────┐
                 │     VCN     │  10.0.0.0/16
                 └──────┬──────┘
           ┌────────────┴────────────┐
     [Public Subnet]           [Private Subnet]
           │                          │
   [Compute Instance]          (reserved)
    VM.Standard.E2.1.Micro

     [Object Storage Bucket] ── (dummy sensitive data)

     [IAM: Compartments / Groups / Policies]
```

*(Diagram to be replaced with an actual draw.io export — see `/screenshots`)*

## Methodology

| Phase | What I did |
|---|---|
| 1. Build | Provisioned VCN, subnet, compute instance, object storage bucket, IAM compartments/groups |
| 2. Break | Introduced 4 realistic misconfigurations (overly broad IAM policy, open SSH ingress, public bucket, disabled Cloud Guard) |
| 3. Detect | Used OCI Cloud Guard + manual CLI verification to identify each issue |
| 4. Assess | Scored each finding by Likelihood × Impact, mapped to CIS OCI Benchmark controls |
| 5. Remediate | Applied least-privilege fixes and re-verified |

Full write-up for each phase is in this repo:
- [`01-environment-setup.md`](./01-environment-setup.md)
- [`02-misconfigurations.md`](./02-misconfigurations.md)
- [`03-detection-cloudguard.md`](./03-detection-cloudguard.md)
- [`04-risk-register.md`](./04-risk-register.md)
- [`05-remediation.md`](./05-remediation.md)

## Key findings (summary)

| Finding | CIS Control | Risk Rating |
|---|---|---|
| IAM policy grants `manage all-resources` to Developers group | CIS 1.1 | Critical |
| SSH open to 0.0.0.0/0 on port 22 | CIS 2.1 | High |
| Public storage bucket | CIS 4.1 | High |
| Cloud Guard disabled | CIS 3.1 | Medium |

Full risk register with likelihood/impact scoring and remediation notes: [`04-risk-register.md`](./04-risk-register.md)

## Skills demonstrated

- OCI IAM (compartments, groups, policies, least privilege)
- OCI networking (VCN, subnets, security lists)
- Cloud Guard / native cloud security tooling
- CIS Benchmark mapping and compliance reporting
- Risk scoring methodology (Likelihood × Impact)
- OCI CLI

## About me

Cybersecurity student at ENSA Agadir, focused on offensive security and secure development. See my other projects: [Active Directory pentest engagement](#) · [Tralalero – secure e-commerce platform](https://github.com/yassinekharouai/tralalero)
