<div align="center">

<img src="assets/kubernetes-course-banner.png" alt="Kubernetes Zero to Production — Learn, Build, Troubleshoot, Operate" width="100%" />

# Kubernetes Zero to Production

**Learn Kubernetes from the basics, build real applications, and understand how to operate them in production.**

[![Kubernetes](https://img.shields.io/badge/Kubernetes-Learning_Path-326CE5?logo=kubernetes&logoColor=white)](https://kubernetes.io/docs/home/)
[![Hands-on](https://img.shields.io/badge/Approach-Hands--on-15803D)](#how-to-use-this-repository)
[![Level](https://img.shields.io/badge/Level-Beginner_to_Advanced-7C3AED)](#course-roadmap)

</div>

## Welcome

I put this repository together for anyone who wants to understand Kubernetes beyond memorizing commands or YAML files.

We'll start with a simple application and the problems that appear as it grows: container failures, traffic spikes, deployments, and managing workloads across multiple machines. From there, we'll explore how Kubernetes works internally, set up clusters, deploy applications, and troubleshoot them.

The goal is to understand **what we're doing, why we're doing it, and how to verify that it works**.

> **How I teach:** We begin with the problem, draw the architecture, understand the components, and then try it ourselves.

## What you'll learn

| 🧠 Understand | 🛠️ Build | 🔎 Troubleshoot | 🚀 Operate |
|:---|:---|:---|:---|
| Kubernetes architecture, workloads, networking and storage | Clusters, manifests, deployments, services and Helm charts | Pods, scheduling, DNS, networking, resources and application failures | Security, observability, GitOps, scaling and production practices |

## Course roadmap

This course is organized in stages. I'll add notes, diagrams, and lab files as each lesson is published.

| Stage | Topics | Status |
|:---|:---|:---|
| **01 — Getting started** | Why Kubernetes? Containers, orchestration and core terminology | In preparation |
| **02 — Architecture** | Control plane, worker nodes, API server, etcd, scheduler, controllers, kubelet | Planned |
| **03 — Cluster setup** | Local clusters, kubeadm and managed Kubernetes concepts | Planned |
| **04 — Workloads** | Pods, ReplicaSets, Deployments, DaemonSets, StatefulSets, Jobs | Planned |
| **05 — Networking** | Services, DNS, Ingress, Gateway API, CNI and NetworkPolicies | Planned |
| **06 — Configuration & storage** | ConfigMaps, Secrets, volumes, PVs, PVCs and StorageClasses | Planned |
| **07 — Security** | RBAC, service accounts, security contexts and workload isolation | Planned |
| **08 — Reliability & troubleshooting** | Probes, resource management, autoscaling, observability and incident scenarios | Planned |
| **09 — Delivery & operations** | Helm, GitOps, upgrades, backups and operational practices | Planned |
| **10 — Production projects** | End-to-end deployments and realistic troubleshooting exercises | Planned |

## Start here

### 🎬 Lesson 01 — Why do we need Kubernetes?

Before learning what a Pod or Deployment is, let's understand the problems that led to Kubernetes in the first place.

We'll use an online shopping application to explore:

- What happens when a container crashes?
- How do we handle more users without managing everything manually?
- What if a server goes down?
- How can we release a new application version safely?
- Which of these problems does Kubernetes help us solve—and what does it *not* solve automatically?

**Lesson notes:** Coming with Video 01.  
**Video:** Coming soon.

## How to use this repository

1. **Follow the video** for the explanation and architecture walkthrough.
2. **Open the lesson README** to review the diagrams and key concepts.
3. **Run the lab commands** when a lesson includes a practical exercise.
4. **Check the expected output** instead of assuming a command succeeded.
5. **Try the troubleshooting questions** before looking at the explanation.

The diagrams are part of the notes, so you can learn visually without needing a separate slide deck.

## Lab prerequisites

You don't need a Kubernetes cluster for the first lesson. As we move into hands-on topics, I'll list the exact tools and versions for each lab.

Typical tools we'll use include:

- A terminal and a Linux environment
- Docker or another suitable container runtime for container exercises
- `kubectl`
- A local Kubernetes environment or a cloud cluster, depending on the lab
- Git and a code editor

> **Cloud cost reminder:** Some labs may create billable resources. I'll identify those labs and include cleanup instructions. Always review the resources before creating them.

## Useful references

- [Kubernetes documentation](https://kubernetes.io/docs/home/)
- [Kubernetes concepts](https://kubernetes.io/docs/concepts/)
- [kubectl reference](https://kubernetes.io/docs/reference/kubectl/)

---

**Learn the concept. Understand the architecture. Practice the commands. Troubleshoot the failures.**
