# Project 04 — ConfigMaps, Secrets & CreateContainerConfigError Debugging

## Overview
This project covers how to manage application configuration and sensitive credentials in Kubernetes using ConfigMaps and Secrets, and how to debug one of the most common silent failures — a Pod that cannot start because it references a resource that does not exist.

## What this project covers
- Creating a ConfigMap with environment variables
- Creating a Secret with base64-encoded credentials
- Injecting both into a Deployment using envFrom
- Verifying environment variables inside a running container
- Debugging CreateContainerConfigError with kubectl describe
- Fixing a missing ConfigMap reference and verifying recovery

## Why this matters in production
No production system hardcodes credentials or configuration in container images. ConfigMaps and Secrets are the Kubernetes-native way to separate configuration from code — mandatory in any team following security best practices. A missing ConfigMap reference is a silent failure that blocks Pod startup with no obvious error on apply — knowing how to diagnose it quickly prevents extended outages.

## Tech stack
- Kubernetes via Minikube
- Vim
- kubectl

## Files
- `configmap.yaml` — ConfigMap with APP_ENV, APP_VERSION and LOG_LEVEL
- `secret.yaml` — Secret with DB_PASSWORD and API_KEY in base64
- `deployment.yaml` — Deployment injecting both ConfigMap and Secret via envFrom

## Commands used
```bash
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f deployment.yaml
kubectl get configmaps
kubectl get secrets
kubectl get pods
kubectl exec -it <pod-name> -- env | grep -E "APP_ENV|DB_PASSWORD"
kubectl describe pod <pod-name>
```

## Key concepts
- **ConfigMap**: stores non-sensitive configuration as key-value pairs injected into Pods as environment variables or mounted as files
- **Secret**: stores sensitive data base64-encoded — Kubernetes decodes automatically when injecting into the container
- **envFrom**: injects all key-value pairs from a ConfigMap or Secret as environment variables in one block
- **CreateContainerConfigError**: Pod cannot start because a referenced ConfigMap or Secret does not exist in the namespace
- **base64**: encoding scheme used for Secret values — not encryption, just encoding
