# Project 01 — Creating Your First Kubernetes Pod with Vim & Minikube

## Overview
This project covers the fundamentals of Kubernetes by deploying a first Pod manually using a YAML manifest written entirely in Vim. No shortcuts, no generators — raw manifest from scratch.

## What this project covers
- Configuring Vim for Kubernetes YAML editing
- Understanding Pod anatomy line by line
- Writing and applying a Pod manifest
- Verifying Pod status and debugging common errors
- Understanding YAML indentation requirements

## Why this matters in production
A Pod is the smallest deployable unit in Kubernetes. Every container running in a production cluster lives inside a Pod. Engineers who cannot read and write Pod manifests by hand cannot effectively debug production incidents — which is where the real cost of downtime lives.

## Tech stack
- Kubernetes via Minikube
- Vim
- kubectl

## Files
- `pod.yaml` — Pod manifest running nginx:latest on port 80

## Commands used
```bash
kubectl apply -f pod.yaml
kubectl get pods
kubectl describe pod first-pod
kubectl logs first-pod
```

## Key concepts
- **Pod**: smallest deployable unit in Kubernetes, wraps one or more containers sharing network and storage
- **apiVersion**: defines which Kubernetes API handles this resource
- **kind**: the resource type being created
- **metadata**: name and labels used to identify and select the resource
- **spec**: defines the desired state — containers, images, ports
