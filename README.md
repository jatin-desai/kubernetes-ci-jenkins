# kubernetes-ci-jenkins

Option 1: Deploy as docker container
```
docker run -p 8080:8080 -p 50000:50000 -v /var/run/docker.sock:/var/run/docker.sock  -v $(which docker):/usr/bin/docker -v /Users/shared/sandbox/jenkins_home:/var/jenkins_home jatindesai/jenkins:lts-alpine

cat /Users/shared/sandbox/jenkins_home/secrets/initialAdminPassword
```

Option 2: Deploy to Kubernetes cluster
```
kubectl create namespace kube-ci; kubectl apply -f jenkins.yml; kubectl rollout status deployment/jenkins -n=kube-ci

kubectl exec -it `kubectl get pods --selector=app=jenkins --output=jsonpath={.items..metadata.name}` cat /var/jenkins_home/secrets/initialAdminPassword

```
