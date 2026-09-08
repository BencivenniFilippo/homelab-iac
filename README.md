# 🏡 Bare-Metal K3s Homelab

Welcome to my Infrastructure as Code (IaC) repository. This repo contains the declarative configuration for my personal bare-metal Kubernetes cluster. It is entirely managed via **GitOps** principles, meaning this repository acts as the single source of truth for the cluster's state.

## 🏗️ Architecture & Tech Stack

This cluster is designed to emulate production-grade Platform Engineering and SRE practices on a smaller, bare-metal scale. 

| Component | Technology | Purpose |
| :--- | :--- | :--- |
| **Orchestration** | **K3s** | Lightweight Kubernetes distribution running on bare-metal Linux. |
| **GitOps / CI/CD** | **ArgoCD** | Monitors this Git repository and automatically synchronizes the cluster state to match the declarative manifests. |
| **Networking & VPN** | **Tailscale** | WireGuard-based mesh VPN providing zero-trust secure access to the cluster nodes and internal services. |
| **Ingress & TLS** | **NGINX Ingress** | Handles incoming traffic routing, automatically paired with **Let's Encrypt** for automated TLS certificate provisioning and rotation. |
| **DNS Management**| **Blocky** | Fast and lightweight DNS proxy for local service discovery and network-level filtering. |
| **Stateful Workload**| **Nextcloud** | Self-hosted cloud storage. Acts as the primary stateful application to manage Persistent Volume Claims (PVCs) and database state.
| **Disaster Recovery**| **Velero** | Automates cluster state and persistent volume backups, offloading encrypted snapshots to a **Backblaze B2** S3-compatible bucket. |

## 🚀 Why I Built This

I built this infrastructure to bridge the gap between application development (MLOps/Backend) and platform reliability. By running bare-metal Kubernetes, I bypass managed cloud abstractions (like GKE or EKS) to get hands-on experience with fundamental infrastructure challenges:

* **Declarative Infrastructure:** No manual `kubectl apply`. If the cluster goes down, ArgoCD can rebuild the entire state from this repository.
* **Security & Zero-Trust:** Management interfaces are not exposed to the public internet; everything is routed securely through Tailscale.
* **Operational Readiness:** Velero ensures I have tested and automated recovery pipelines (RPO/RTO) for stateful applications.
