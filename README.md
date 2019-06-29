# canary-release-demo
1 Install kustomize(about kustomize : https://github.com/kubernetes-sigs/kustomize)

        go get github.com/kubernetes-sigs/kustomize
  
  
2 Create namespace in local minikube:
  
        kubectl create namespace ingress-nginx
  
3 set ingress-nginx as current namespace

        kubectl config set-context $(kubectl config current-context) --namespace=ingress-nginx
  
4 create serviceaccount for nginx-ingress or traefik(about rbac : https://kubernetes.github.io/ingress-nginx/deploy/rbac/)

        kubectl apply -k rbac/
  
5 create app and app-canary you can change your own app image in app/deployment.yaml, app-canary/deploymeny.yaml

        kubectl apply -k app/
  
        kubectl apply -k app-canary/
  
6 create nginx ingress controller or traefik

        nginx : kubectl apply -k nginx-ingress-controller/
  
        traefik : kubectl apply -k traefik-ingress-controller/
  
7 create nginx ingress or traefik resource

        nginx : kubectl apply -f nginx-ingress-resource/
  
        traefik : kubectl apply -f traefik-ingress-resource/
        
nginx ingress controller need host to do canary release , so when you use nginx , you need add host (app.com)
and add it to your local hosts file ,ip is minikube's ip.
  
