# webapp-bot-infrastructure

### Project Overview
This repository documents the infrastructure and deployment pipeline for a high-availability Discord bot and web application. The project serves as a "Proving Ground" for mastering cloud architecture, security protocols, and automated lifecycle management.

### Core Technology Stack
* **Orchestration:** Azure Kubernetes Service (AKS)
* **CI/CD:** GitHub Actions (Self-Hosted Runner architecture)
* **Containerization:** Docker & Azure Container Registry (ACR)
* **Automation:** Jira API Integration for real-time security alerting
* **Scripting:** PowerShell (Infrastructure) & Python (Application Logic)

---

### Engineering Challenges & Solutions

**Tenant Permission Constraints:** Encountered restricted Entra ID (Azure AD) privileges on an educational subscription that prevented the creation of standard Service Principals.
**Security vs. Automation:** To bypass tenant blocks safely, I implemented a **Self-Hosted Runner** on a local private agent. This allowed for authenticated deployments without exposing the build environment to the public.
**Public Portfolio Security:** Adhered to a **Zero-Trust model** by utilizing a Private-Public split. Sensitive deployment logic and CI/CD runners are kept in a private repository, while this infrastructure map serves as a public-facing audit of the work. 

---

### SDLC & Security Posture

* **Secrets Management:** Utilizing Kubernetes Secrets to inject sensitive API tokens (Discord, Spotify, Jira) at runtime, ensuring no plaintext credentials exist in the source code.
* **Immutable Infrastructure:** Employing Docker to ensure environment parity between local development and the AKS production cluster.
* **Rolling Updates:** Utilizing `kubectl rollout` strategies to ensure zero-downtime when pushing bot updates or rotating API keys.
