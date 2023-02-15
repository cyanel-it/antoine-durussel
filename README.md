# Kubernetes

## Practice 1

Create deployment and service :
```bash
kubectl apply -f practice-1/nginx-deployment.yaml
kubectl apply -f practice-2/nginx-service.yaml
```

Clean:
```bash
kubectl delete deployment nginx-deployment
kubectl delete service nginx-service
```

## Practice 2

Before started, create namespaces :
```bash
sh practice-2/bin/create_guestbook_ns.sh
```

Create Redis leader deployment and service, Redis follower ones and frontend ones :
```bash
kubectl apply -f practice-2/redis-leader-deployment.yaml
kubectl apply -f practice-2/redis-leader-service.yaml
kubectl apply -f practice-2/redis-follower-deployment.yaml
kubectl apply -f practice-2/redis-follower-service.yaml
kubectl apply -f practice-2/frontend-deployment.yaml
kubectl apply -f practice-2/frontend-service.yaml
```

Forward frontend to see application on http://localhost:8080:
```bash
kubectl port-forward svc/frontend 8080:80
```

Scale and unscale number of pods:
```bash
kubectl scale deployment frontend --replicas=5
kubectl scale deployment frontend --replicas=2
```

Clean:
```bash
kubectl delete deployment -l app=redis
kubectl delete service -l app=redis
kubectl delete deployment frontend
kubectl delete service frontend
```

## Practice - Persistent volumes

Before started :
```bash
minikube ssh
sudo mkdir /mnt/data
sudo sh -c "echo 'Hello from Kubernetes storage' > /mnt/data/index.html"
```

Then create persistent volume, persistent volume claim and pod using this claim :
- Persistent volume
- Persistent volume claim
- Pod using persistent volume claim

```bash
kubectl apply -f practice-persistent-volumes/pv-volume.yaml
kubectl apply -f practice-persistent-volumes/pv-claim.yaml
kubectl apply -f practice-persistent-volumes/pv-pod.yaml
```

Clean :
```bash
kubectl delete pod task-pv-pod
kubectl delete pvc task-pv-claim
kubectl delete pv task-pv-volume

minikube ssh
sudo rm /mnt/data/index.html
sudo rmdir /mnt/data
```


