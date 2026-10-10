# Day 01 — Why Do We Need Kubernetes?

> **Kubernetes Zero to Production · Video 01**  
> Today we'll start with a normal application, see where managing containers manually becomes difficult, and understand why Kubernetes exists.

![Day 01: Kubernetes at a glance](images/00-lesson-overview.png)

## What we're going to understand

- What changes when an application grows beyond one container and one server?
- What happens when containers or servers fail?
- Why do we need multiple application instances and controlled updates?
- What exactly does Kubernetes manage—and what still needs to be configured by us?

---

## 1. Start with one application

Imagine we're running an online shopping application. At first, the setup is straightforward: one Linux server and one application container. Users open the website, requests reach the server, and the application responds.

![Users access an application container running on a Linux server](images/01-single-server.png)

**This isn't a bad design for learning or small workloads.** But if that one container or server stops working, there may be nothing else available to handle the requests.

**Think about it:** Who notices when the application stops responding? How quickly can we restore it?

## 2. What if the container crashes?

A container might exit because the application has a bug, its process crashes, or it runs out of memory. If nothing is configured to restart it, the application stays unavailable until someone intervenes.

![A failed application container interrupts requests](images/02-container-failure.png)

On a standalone Docker host, we can configure restart policies. Kubernetes goes further: it continually works toward the **desired state** we declare, using controllers and node agents to maintain workloads.

**Important:** Kubernetes doesn't fix the bug that caused the crash. A repeatedly failing application can still enter `CrashLoopBackOff`.

## 3. What happens when traffic increases?

Now imagine a festival sale. The same application receives many more requests than usual. A single instance may no longer have enough CPU, memory, or throughput.

![Traffic is distributed across multiple application instances](images/03-traffic-and-scaling.png)

One approach is to run multiple instances and put a load balancer in front of them. But then we have more questions:

- Where should each instance run?
- How do we keep the right number of instances running?
- How do we avoid sending traffic to instances that aren't ready?

Kubernetes can maintain a chosen number of replicas and work with Services to route traffic to ready endpoints. **Automatic scaling based on metrics requires additional configuration**, such as the Horizontal Pod Autoscaler and suitable metrics.

## 4. What if an entire server goes down?

Running several containers on a single server doesn't protect us from that server failing. We need multiple machines and a way to run replacement workloads on healthy machines.

![A server failure requires healthy capacity elsewhere](images/04-server-failure.png)

With multiple worker nodes, Kubernetes can replace certain workloads on available healthy nodes. This depends on spare capacity, scheduling rules, storage behavior, and application design. It isn't an instant or unconditional guarantee of zero downtime.

## 5. What about releasing a new version?

Suppose the shopping app needs a checkout update. Replacing every running instance at once could interrupt users.

A Kubernetes **Deployment** supports rolling updates: new Pods are introduced while older Pods are gradually removed, subject to the update strategy. **Readiness probes, sufficient replicas, capacity, and application behavior** all matter if we want users to experience minimal disruption.

## 6. So, what is Kubernetes?

**Kubernetes is an open-source container orchestration platform.** We describe the state we want—such as an application running with three replicas—and Kubernetes components work continuously to bring the actual state closer to it.

![Users, load balancer, Kubernetes control plane and worker nodes](images/05-kubernetes-cluster.png)

A very high-level view:

| Part | What it does |
|---|---|
| **Control plane** | Exposes the Kubernetes API, stores cluster state, schedules Pods, and runs controllers |
| **Worker nodes** | Run application Pods using the kubelet and container runtime |
| **Deployment** | Describes and manages replicated stateless application workloads |
| **Service** | Provides a stable way to reach a changing set of Pods |

We'll explore these components individually in the architecture lessons. For now, focus on the main idea: **we declare the desired state; Kubernetes keeps reconciling toward it.**

## 7. What Kubernetes does *not* do automatically

- It doesn't repair broken application code.
- It doesn't automatically scale every application without configuration.
- It doesn't guarantee zero downtime just because we use a Deployment.
- It doesn't make a single-node cluster highly available.
- It doesn't replace the need for monitoring, security, backups, or good architecture.

## Quick recap

| Challenge | How Kubernetes can help |
|---|---|
| Container exits | Restarts or replaces workload containers/Pods according to configuration |
| Need multiple copies | Maintains desired replicas through workload controllers |
| Traffic to changing Pods | Services provide stable discovery and routing |
| Worker node fails | Can schedule replacement Pods on healthy nodes when possible |
| New application version | Deployments support controlled rolling updates and rollbacks |

### Check your understanding

1. If a container crashes, does Kubernetes fix the underlying application bug?
2. If a cluster has only one worker node, can Kubernetes keep the application running after that node fails?
3. What's the difference between running three replicas and automatically scaling replicas?
4. Why do readiness probes matter during a rolling update?

**Next:** Containers, Kubernetes basics, and the components inside a cluster.

---

*Diagrams are included in this folder for learning and presentation. The overview is conceptual, not a literal network topology or complete production design.*
