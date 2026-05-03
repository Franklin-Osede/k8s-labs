# Project 03 — Kubernetes Services: NodePort & Selector Debugging

## Overview
This project covers how to expose a Kubernetes application to external traffic using Services, and how to debug one of the most common and silent production failures — a selector mismatch that leaves Endpoints empty and the app unreachable.

## What this project covers
- Creating a NodePort Service to expose nginx externally
- Accessing the application from the browser via Minikube
- Understanding selector-to-label matching
- Debugging SVC_UNREACHABLE with kubectl describe and kubectl get endpoints
- Fixing a selector mismatch and verifying recovery

## Why this matters in production
A Service with a wrong selector creates a silent failure — kubectl apply returns no errors, the Service exists, the Pods are running, but traffic never reaches them. This is one of the most common misconfiguration patterns in teams new to Kubernetes. Knowing how to go straight to kubectl get endpoints is what separates engineers who debug this in 30 seconds from those who spend hours checking the wrong things.

## Tech stack
- Kubernetes via Minikube
- Vim
- kubectl

## Files
- `service.yaml` — NodePort Service exposing nginx on port 30080

## Commands used
```bash
kubectl apply -f service.yaml
kubectl get services
minikube service nginx-service
kubectl describe service nginx-service
kubectl get endpoints nginx-service
```

## Key concepts
- **Service**: stable networking endpoint that routes traffic to Pods matching a selector
- **NodePort**: exposes the Service on a static port on the Node, accessible from outside the cluster
- **Selector**: key-value label that the Service uses to find target Pods
- **Endpoints**: list of Pod IPs the Service is actively routing traffic to — if empty, the selector does not match any running Pod
- **SVC_UNREACHABLE**: Service exists but has no healthy Pods behind it — always check Endpoints first
