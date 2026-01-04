# cicd-jenkins-kubernetes

## How to use

I followed dthis [tutorial](https://medium.com/@jaiymzndubuisi/a-step-by-step-guide-to-ci-cd-with-jenkins-github-and-kubernetes-7b8090146a07) for the configuration of the env

delete old kubernetes elements

```bash
kubectl delete all -l app=hellodocker-deployment
kubectl delete deployment hellodocker-deployment
kubectl delete service hellodocker-service
```

run the pipeline and then ```minikube service hellodocker-service```
