# Devops

## Python

```shell
python3 
python3 --version

# install dependencies
python3 -m venv ~/.venv
source ~/.venv/bin/activate
pip3 install -r requirements.txt


python3 python-app/src/app.py

# Docker

docker pull python:3.12-alpine
docker images
docker build -t python-app:v1 .
docker run -p 8080:5000 python-app:v1

docker push salvamoyanopalma/python-app:tagname
docker login -u salvamoyanopalma


docker tag python-app:v1 salvamoyanopalma/python-app:v1

docker push salvamoyanopalma/python-app:v1

# Kubernetes

kind --version
kubectl version
kubectl get pods
kubectl cluster-info
kubectl get ns

kind crete cluster --config k8s/ingress/kind-config.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

kubectl get pods -n ingress-nginx

kubectl get deployments
kubectl delete -f deploy.yaml

# Esto es para poder utilizar repository docker hub private
kubectl create secret docker-registry regcred \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=salvamoyanopalma \
  --docker-password= \
  --docker-email=salvamoyanopalma@gmail.com

kubectl apply -f deploy.yaml
kubectl get deployments
kubectl get pods 
kubectl apply -f service.yml
kubectl get svc
kubectl describe svc python-app
kubectl get ingressclass
kubectl apply -f ingress.yaml
kubectl get ing

nano /etc/hosts
# Añadir
127.0.0.1 python-app.test.com

kubectl delete -f ingress.yaml
kubectl delete -f service.yaml
kubectl delete -f deploy.yaml
kubectl delete namespace python

# Helm 
helm version
helm create python-app
kubectl create namespace python
kubectl create secret docker-registry regcred \
  --docker-server=https://index.docker.io/v1/ \
  --docker-username=salvamoyanopalma \
  --docker-password= \
  --docker-email=salvamoyanopalma@gmail.com \
  --namespace=python
helm install python-app -n python . 

helm repo add argo https://argoproj.github.io/argo-helm
helm repo ls

helm upgrade --install argocd argo/argo-cd -n argocd --create-namespace -f values-argo.yaml
kubectl get pods -n argocd
kubectl get ing -n argocd
kubectl get ing -n argocd -o yaml

kubectl get pods -n argocd
kubectl get secrets -n argocd
kubectl get secrets -n argocd argocd-initial-admin-secret -o yaml
echo cUhLMXk4NFhUbkctSUc2RA== | base64 -d -> qHK1y84XTnG-IG6D

#Token 
git remote add origin https://github.com/salva-moyano/mpr-backstage.git
git remote set-url origin https://salvamoyanopalma:TU_TOKEN@github.com/salva-moyano/mpr-backstage.git

# Hacer un reset de una rama 
git checkout --orphan nueva_rama
git add .
git commin -m "initial commit"
git branch -D ${BRANCHE}
git branch -m ${BRANCHE}
git push orgin ${branch} --force

# Verificar que no queda nada en el historial

git log --oneline

# Proble with argocd
kubectl patch configmap argocd-rbac-cm -n argocd \        
  --type merge \
  -p '{
    "data": {
      "policy.default": "role:admin",
      "policy.csv": "g, admin, role:admin\np, role:admin, applications, sync, */*, allow\np, role:admin, applications, get, */*, allow\np, role:admin, applications, update, */*, allow"
    }
  }'
kubectl get configmap argocd-rbac-cm -n argocd -o yaml  

Debe mostrar:
yamldata:
  policy.default: role:admin
  policy.csv: |
    g, admin, role:admin
    p, role:admin, applications, sync, */*, allow
    p, role:admin, applications, get, */*, allow
    p, role:admin, applications, update, */*, allow
    
kubectl rollout restart deployment argocd-server -n argocd
kubectl rollout status deployment argocd-server -n argocd

#Backstage

docker images
docker pull node:22-alpine

docker run --rm -p 3000:3000 -ti -v /Users/smoyano/dev/devops/backstage/backstage-app:/app -w /app node:22 bash

docker run --rm -e AUTH_GITHUB_CLIENT_ID=  -e AUTH_GITHUB_CLIENT_SECRET= -e GITHUB_TOKEN=  -p 3000:3000 -p 7007:7007 -ti -v /Users/smoyano/dev/devops/backstage/backstage-app:/app -w /app node:22 bash


npx @backstage/create-app@latest
yarn start

https://backstage.io/docs/auth/



yarn --cwd packages/backend add @backstage/plugin-auth-backend-module-github-provider

https://github.com/backstage/backstage/blob/master/packages/catalog-model/examples/acme/team-a-group.yaml

https://backstage.io/docs/features/software-catalog/descriptor-format/#kind-component


#Dockerfile

FROM node:18-bookworm-slim
 
RUN apt-get update && apt-get install -y python3 python3-pip python3-venv
 
ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"
 
RUN pip3 install mkdocs-techdocs-core

# Template

http://localhost:3000/create/actions

https://backstage.io/docs/features/software-templates/builtin-actions

```

¿Qué es IDP?