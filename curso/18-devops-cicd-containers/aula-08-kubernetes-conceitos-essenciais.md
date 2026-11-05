# Aula 8 — Kubernetes: conceitos essenciais

**Duração:** ~30 min · **Módulo 18**

## Objetivo
Conhecer os objetos básicos do Kubernetes e implantar uma aplicação.

## Teoria
- **Cluster** = *control plane* (API server, scheduler, etcd, controllers) + **nodes** (kubelet, runtime).
- **Pod**: menor unidade; um ou mais containers com rede e volumes compartilhados. Efêmero.
- **Deployment**: mantém N réplicas e faz rolling updates (via ReplicaSet).
- **Service**: IP/DNS estável que balanceia entre pods (ClusterIP, NodePort, LoadBalancer).
- **Ingress**: roteamento HTTP externo. **ConfigMap/Secret**: configuração. **Namespace**: isolamento lógico.
- Modelo **declarativo**: você descreve o estado desejado; controllers reconciliam.
- **Probes**: liveness (reinicia), readiness (recebe tráfego). **requests/limits** definem recursos.
- **HPA**: escala réplicas por CPU/métricas.

## Exemplo
```yaml
apiVersion: apps/v1
kind: Deployment
metadata: { name: api }
spec:
  replicas: 3
  selector:
    matchLabels: { app: api }
  template:
    metadata:
      labels: { app: api }
    spec:
      containers:
        - name: api
          image: ghcr.io/org/api:1.0.0
          ports: [{ containerPort: 8000 }]
          envFrom:
            - configMapRef: { name: api-config }
          resources:
            requests: { cpu: 100m, memory: 128Mi }
            limits: { memory: 256Mi }
          readinessProbe:
            httpGet: { path: /health, port: 8000 }
          livenessProbe:
            httpGet: { path: /health, port: 8000 }
            initialDelaySeconds: 10
---
apiVersion: v1
kind: Service
metadata: { name: api }
spec:
  selector: { app: api }
  ports: [{ port: 80, targetPort: 8000 }]
```
```bash
kubectl apply -f api.yaml
kubectl get pods -l app=api
kubectl scale deployment api --replicas=5
kubectl logs deploy/api
kubectl port-forward svc/api 8080:80
```

## Exercício
1. Suba um cluster local (kind ou minikube), aplique o manifesto e acesse via `port-forward`.
2. Delete um pod e observe o Deployment recriá-lo. Explique por quê.

## Checklist
- [ ] Conheço Pod, Deployment, Service e Ingress
- [ ] Entendo o modelo declarativo
- [ ] Defino probes e resources
