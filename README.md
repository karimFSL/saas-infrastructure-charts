# creater load balancer
kubectl expose deployment hello-world --type=LoadBalancer --name=hello-world-service-loadbalancing --port=8080 --target-port=8080 -n demo


# tester template helm
helm template nginx ./helm-for-dev-chart --set-string namespace=helm-for-dev -s templates/namespace.yaml


# install helm
helm install helm-for-dev-2 ./helm-for-dev-chart --set-string namespace=helm-for-dev-2-ns --set image=wilda/app2

# modif helm
helm upgrade helm-for-dev-2 ./helm-for-dev-chart --set-string namespace=helm-for-dev-2-ns --set image=wilda/app2 --set env[0].name=LOG_LEVEL,env[0].value=info

# deletion 
helm delete helm-for-dev-1



# list artifact hub
https://artifacthub.io/packages/search?kind=0&sort=relevance&page=1



# install k3s master
curl -sfL https://get.k3s.io | sh -

# add node
curl -sfL https://get.k3s.io | K3S_URL=https://serverip:6443 K3S_TOKEN=mytoken sh -
mytoken at location => /var/lib/rancher/k3s/server/node-token


# plus besoin de sudo pour kubectl
mkdir -p $HOME/.kube
sudo cp /etc/rancher/k3s/k3s.yaml $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# helm command
helm repo add my-repo-name http://my-repo-url
helm repo update

# lister charts 
 `helm search repo`

# install charts sur un cluster => release
 `helm install webserver-001 my-repo-name/my-web-server`
 $ helm install -f values.yaml bitnami/wordpress --generate-name

Helm va alors effectuer les actions suivantes :

télécharger l’archive “my-web-server” depuis le registre “my-repo-name”
merger les éventuelles valeurs données en ligne de commande avec les valeurs par défaut du Chart - ici, pas de surcharges, on utilise seulement les valeurs par défaut
générer les manifestes à installer depuis les templates
installer ces manifestes sur le cluster dans le namespace en cours / spécifié.
inscrire ces manifestes dans un fichier d’état ; par défaut, ce fichier d’état est dans un secret Kubernetes.

# upgrade
```helm upgrade webserver-001 my-little-repo/my-web-server -f values_webserver_001.yaml```

# list release helm
helm ls

# uninstall release
`helm uninstall webserver-001`.

# status release deployed sur le cluster
helm status happy-panda

# values de la release
helm get values happy-panda


# show values 
helm show values bitnami/wordpress

# rollback
helm rollback [RELEASE_NAME] [VERSION]