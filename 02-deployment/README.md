# Project 02 — Deployment, Rolling Updates, Rollbacks & Debugging

## Overview
This project demonstrates how to manage application lifecycle in Kubernetes using Deployments. Covers the full production workflow — deploying, updating, rolling back, and debugging real failures — all from the terminal using Vim.

## What this project covers
- Creating a Deployment with 3 replicas
- Self-healing — automatic Pod replacement on failure
- Rolling update with zero downtime
- Rollback to previous version in seconds
- Debugging ImagePullBackOff with kubectl describe
- Using Vim search and replace to update manifests efficiently

## Why this matters in production
In any company running Kubernetes, Deployments are the standard unit for managing applications. Rolling updates guarantee zero downtime during releases. Rollbacks are the immediate response when a bad deploy hits production at 3am. Engineers who cannot execute these operations confidently under pressure are a liability in any on-call rotation.

## Tech stack
- Kubernetes via Minikube
- Vim
- kubectl

## Files
- `deployment.yaml` — Deployment manifest with 3 replicas running nginx

## Commands used
```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl delete pod <pod-name>
kubectl rollout status deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment
kubectl rollout history deployment/nginx-deployment
kubectl describe pod <pod-name>
```

## Key concepts
- **Deployment**: manages a ReplicaSet which maintains the desired number of Pod replicas at all times
- **ReplicaSet**: watches over Pods and replaces them automatically if they fail
- **Rolling update**: updates Pods one by one — never takes all replicas down simultaneously
- **Rollback**: reverts to the previous Deployment revision instantly
- **ImagePullBackOff**: Kubernetes cannot pull the container image — check image name and tag
