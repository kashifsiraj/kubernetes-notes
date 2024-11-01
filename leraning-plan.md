# CKAD Certification Learning Plan
## Week 1: Core Concepts and Pod Design
- [ ] **Days 1-3:** Learn Kubernetes architecture, key commands (kubectl basics).
- [ ] **Days 4-7:** Dive into Pods, Deployments, ReplicaSets, and Namespaces.
- [ ] **Project:** Set up a Namespaces-based multi-tenant cluster.

## Week 2: Multi-Container Pods and Configuration
- [ ] **Days 1-3:** Practice multi-container patterns with sidecars and init containers.
- [ ] **Days 4-7:** Study ConfigMaps, Secrets, environment variables.
- [ ] **Project:** Build a web app with logging and monitoring sidecars.

## Week 3: Observability, Services, and Networking
- [ ] **Days 1-3:** Learn Logs, Events, Metrics, and Probes.
- [ ] **Days 4-7:** Focus on Services and Networking with Service types and Ingress.
- [ ] **Project:** Deploy a complete multi-tier application with frontend and backend, exposing via Ingress.

## Week 4: State Persistence and Exam Preparation
- [ ] **Days 1-2:** Study PVs, PVCs, StatefulSets, and StorageClasses.
- [ ] **Days 3-5:** Go over troubleshooting and debugging scenarios.
- [ ] **Days 6-7:** Take mock exams, and review missed areas.


# Project Recommendations for CKAD Practice

- [ ] **Multi-Tier Application with CI/CD:**
Set up a CI/CD pipeline to deploy a multi-tier application with frontend, backend, and database tiers. Use ConfigMaps for configuration and Secrets for sensitive data. Expose it using Ingress.

- [ ] **Logging and Monitoring Stack:**
Deploy a logging and monitoring stack (e.g., ELK or Prometheus and Grafana) as sidecars. This project will give hands-on experience with observability.

- [ ] **Stateful Applications with Persistent Storage:**
Deploy a MySQL database in Kubernetes using StatefulSets and PVs, then simulate failure scenarios to observe how Kubernetes handles pod rescheduling with data persistence.

- [ ] **Resilient Application with Probes and Resource Limits:**
Create a resource-intensive application and configure liveness and readiness probes to simulate failures. Apply resource requests and limits to handle scaling and recovery in resource-constrained environments.

This plan builds a robust understanding of Kubernetes and aligns well with CKAD expectations. Practicing in a sandbox or local Kubernetes cluster will provide real-world exposure, crucial for the exam.
