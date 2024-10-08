#### Créer un registre de container


``az acr create --resource-group training-rldahou-rg --name renaudacr --sku Basic``

``az acr login --name  renaudacr``

``az acr login -n renaudacr --expose-token``

``docker build -t flasapp .``

``docker images``


#### Pour obtenir l’adresse du serveur de connexion, utilisez la commande az acr list et interrogez le loginServer.


``az acr list --resource-group training-rldahou-rg --query "[].{acrLoginServer:loginServer}" --output table``



####  Tag l'image


``docker tag flasapp:latest renaudacr.azurecr.io/flasapp:v1``

#### Transférer les images vers le registre

``docker push renaudacr.azurecr.io/flasapp:v1``

#### Lister les images dans le registre

``az acr repository list --name renaudacr --output table``

#### Créer un cluster Kubernetes

#### Pour permettre à un cluster AKS d'interagir avec d'autres ressources Azure, une identité de cluster est automatiquement créée. Dans cet exemple, l'identité du cluster se voit accorder le droit d'extraire des images de l'instance ACR que vous avez créée dans le didacticiel précédent. Pour exécuter la commande avec succès, vous devez disposer d’un rôle de propriétaire ou d’administrateur de compte Azure dans votre abonnement Azure.


``az aks create --resource-group training-rldahou-rg --name myAKSCluster --node-count 1 --generate-ssh-keys --attach-acr renaudacr``



#### Si vous utilisez Azure Cloud Shell, kubectl est déjà installé. Vous pouvez également l’installer localement à l’aide de la commande az aks install-cli.

``sudo az aks install-cli``

#### Pour configurer kubectl pour qu'il se connecte à votre cluster Kubernetes, utilisez la commande az aks get-credentials. L'exemple suivant obtient les informations d'identification pour le cluster AKS nommé myAKSCluster dans training-rldahou-rg

``az aks get-credentials --resource-group training-rldahou-rg --name myAKSCluster``



#### Pour vérifier la connexion à votre cluster, exécutez kubectl get nodes pour renvoyer une liste de nœuds de cluster.
``kubectl get nodes``



``cd msdocs-python-flask-webapp-quickstart ``

#### Créer un manifest de déploiement.
``nano deployment.yaml``

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 1  # Nombre de répliques de votre application
  selector:
    matchLabels:
      app: myapp  # Étiquette pour sélectionner les pods du déploiement
  template:
    metadata:
      labels:
        app: myapp  # Étiquette pour les pods du déploiement
    spec:
      containers:
        - name: myapp-container
          image: renaudacr.azurecr.io/flasapp:v1  # Remplacez par le nom de votre image Docker
          ports:
            - containerPort: 8000  # Port sur lequel le conteneur Docker écoute
```



#### Créer un manifest de service.
``nano service.yaml``

```
apiVersion: v1
kind: Service
metadata:
  name: myapp-service
spec:
  selector:
    app: myapp  # L'étiquette correspondant à votre application
  ports:
    - protocol: TCP
      port: 80  # Le port du service dans Kubernetes
      targetPort: 8000  # Le port du conteneur Docker
  type: LoadBalancer  #LoadBalancer

```


``kubectl apply -f deployment.yaml``

``kubectl apply -f service.yaml``

``kubectl get svc``

``kubectl get deployment``

``kubectl get pods``


``az aks scale --resource-group training-rldahou-rg --name myAKSCluster --node-count 3``


``az aks get-versions --location "West Europe" --output table``

``az aks show --name myAKSCluster --resource-group training-rldahou-rg --query kubernetesVersion -o tsv``


``az aks upgrade --resource-group training-rldahou-rg --name myAKSCluster --kubernetes-version 1.27.1``

### Supprimer les ressource

``az aks delete --name myAKSCluster --resource-group training-rldahou-rg --yes --no-wait``

``az acr delete --name renaudacr --resource-group training-rldahou-rg --yes --no-wait``




```python

```
