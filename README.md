# Awesome-Environment-Variable-Managers

# Top Environment Variable Managers Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Secrets Management, Environment Configuration & Self-Hosted Credential Security*  
**Last updated: October 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Environment Variable Managers**. These tools enable developers and organizations to store, inject, rotate, and audit secrets—API keys, database credentials, tokens—across development, staging, and production environments, replacing insecure `.env` files and hardcoded values.

**Examples** include Doppler, Infisical, 1Password Secrets Automation, HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, Google Secret Manager, CyberArk Conjur, Bitwarden Secrets Manager, and Akeyless (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, custom secret backends, and transparent credential workflows—ideal for teams that require data sovereignty, avoid per-seat SaaS pricing, and need auditable secret management. The open-source landscape is anchored by **HashiCorp Vault** (dynamic secrets pioneer) and its open-governance fork **OpenBao**, with strong developer-friendly alternatives in **Infisical**, **SOPS**, **dotenvx**, and **direnv** for directory-scoped environment loading.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Doppler](https://www.doppler.com/)**  
  Secrets management platform treating rotation as its core product. Rotated Secrets keeps active and standby credentials alive simultaneously, ensuring zero-downtime swaps. Hosted-only with no self-hosted option . Best for small-to-mid teams that want managed multi-environment secret sync with minimal operational burden.

- **[Infisical Cloud](https://infisical.com/)**  
  SaaS tier of the open-source Infisical platform. Offers a clean web UI, straightforward SDKs, and integrations with GitHub Actions, GitLab CI, Jenkins, AWS, GCP, Azure, and Kubernetes. SOC 2 Type II certified . The free self-hosted edition remains the primary draw for cost-conscious teams.

- **[1Password Secrets Automation](https://1password.com/developers/secrets-management/)**  
  Extends 1Password's password manager into service secrets management. Provides CLI and SDK access to vault-stored credentials. Best for organizations already standardized on 1Password for human credentials.

- **[HashiCorp Vault (HCP Vault Dedicated)](https://www.hashicorp.com/products/vault)**  
  Managed version of Vault for teams that want dynamic secrets and Terraform integration without operating the cluster. Vault's core strength is on-demand credential generation: ask for database access, receive a real short-lived user, and let it expire automatically . Self-managed Vault remains open-source (see below).

- **[AWS Secrets Manager](https://aws.amazon.com/secrets-manager/)**  
  Native AWS secrets store with tight IAM integration and automated rotation for RDS, Redshift, and DocumentDB. Best for AWS-centric architectures but lacks general-purpose dynamic secrets for multi-cloud or on-prem systems .

- **[Azure Key Vault](https://azure.microsoft.com/en-us/products/key-vault/)**  
  Azure-native secrets, keys, and certificate management with Microsoft Entra ID integration. Supports automated rotation workflows but does not natively provide Vault-style dynamic database credentials. Best for Azure-native workloads .

- **[Google Secret Manager](https://cloud.google.com/secret-manager)**  
  GCP's managed secrets service with IAM integration and versioning. Best for organizations running primarily on Google Cloud.

- **[CyberArk Conjur](https://www.conjur.org/)**  
  Enterprise secrets management focused on DevOps and machine identity. Strong for organizations with existing CyberArk investments and privileged access management requirements.

- **[Bitwarden Secrets Manager](https://bitwarden.com/products/secrets-manager/)**  
  Extends Bitwarden's open-source password manager into developer secrets management. CLI and SDK access with a familiar interface. Best for teams already using Bitwarden.

- **[Akeyless](https://www.akeyless.io/)**  
  SaaS-based secrets management platform with a "Vaultless" architecture, dynamic secrets, and just-in-time access. Offers a free tier for small teams.

## Open-Source GitHub Projects

- **[HashiCorp Vault](https://github.com/hashicorp/vault)**  
  The reference implementation for secrets management. Dynamic secrets engine mints short-lived database and cloud credentials on demand, eliminating the need to rotate static passwords . Terraform provider makes credential issuance part of infrastructure pipelines. Self-hosting requires operational investment: HA setup, unseal process, and upgrade cadence . Best for platform engineering teams that need dynamic, multi-cloud credential generation.

- **[OpenBao](https://github.com/openbao/openbao)**  
  Open-governance fork of HashiCorp Vault under the Linux Foundation Edge. Maintains high compatibility with Vault's core API and CLI for commonly used secrets engines and auth methods, making it the lowest-friction migration path for Vault-familiar teams . Supports dynamic secrets for databases and Kubernetes. Best for organizations that want Vault capabilities without vendor governance concerns.

- **[Infisical](https://github.com/Infisical/infisical)**  
  Developer-friendly open-source secrets platform with a clean web UI, SDKs, and a free self-hosted edition with no artificial usage caps . MIT licensed core with SOC 2 Type II certification. Supports secret syncing across environments, Kubernetes operator, and integrations with major CI/CD tools. Dynamic secrets are available in higher-tier commercial offerings and should be validated against requirements . Best for small-to-mid teams that want Vault's self-hosting story without Vault's operational weight.

- **[SOPS (Secrets OPerationS)](https://github.com/getsops/sops)**  
  Mozilla-originated tool for encrypting values within YAML, JSON, ENV, and INI files. Integrates with AWS KMS, GCP KMS, Azure Key Vault, age, and PGP. Supports key groups using Shamir's Secret Sharing to require multiple master keys for decryption . Best for GitOps workflows where encrypted secrets live alongside code in version control.

- **[dotenvx](https://github.com/dotenvx/dotenvx)**  
  Encrypted `.env` file management from the creator of dotenv. Single command encrypts `.env` files with private keys, enabling safe version control of environment configuration. Supports multiple environments (`-f .env.production`) and optional armored key management for team access control . Best for Node.js and JavaScript teams that want to keep the `.env` workflow but eliminate plaintext secrets.

- **[direnv](https://github.com/direnv/direnv)**  
  Shell extension that loads and unloads environment variables based on the current directory. Checks for `.envrc` files in current and parent directories, loading them into a sub-shell and capturing exported variables . Language-agnostic and fast enough to be unnoticeable on each prompt. Best for local development where each project needs isolated environment configuration without cluttering `~/.profile`.

- **[Sealed Secrets (Bitnami)](https://github.com/bitnami-labs/sealed-secrets)**  
  Kubernetes controller and CLI for one-way encrypted secrets. Encrypts secrets into `SealedSecret` resources that are safe to commit to Git; only the controller in the target cluster can decrypt them. Apache 2.0 licensed. Best for Kubernetes-native GitOps workflows where cluster-specific decryption is needed.

### Additional Strong Open-Source Options

- **Vault Agent Injector** — Kubernetes sidecar that authenticates to Vault, fetches secrets, and writes them to files for application consumption without code changes .
- **External Secrets Operator** — Kubernetes operator that syncs secrets from external providers (Vault, Infisical, AWS Secrets Manager, etc.) into Kubernetes Secrets.
- **Frameworks for building custom systems**: Combine **OpenBao** for dynamic database credentials with **SOPS** for encrypted config files in Git, **direnv** for local development environment switching, and **External Secrets Operator** for Kubernetes secret injection. For teams wanting a single platform, **Infisical** provides storage, sync, and Kubernetes integration in one self-hosted package.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Secret management tools vary significantly in operational complexity, dynamic secret capabilities, and cloud provider integration; evaluate based on your infrastructure and compliance requirements.
- Self-hosted solutions require proper backup strategies, unseal key management, and access control auditing.

---

**Made for DevOps engineers, platform teams, security engineers, and developers who believe secrets should never be hardcoded.**  
Let's make environment configuration more secure, auditable, and open.
