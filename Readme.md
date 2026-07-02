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
```