# kubernetes_JesusMariaGomezSalmeron
**Se crea un clúster kubernetes con GKE**
Primero, se configura la zona
```
gcloud config set compute/zone us-central1-a
```
Puede ser que no se haya habilitado la API de Kubernetes, en ese caso se hace con:
```
gcloud services enable container.googleapis.com
```
Acto seguido, se crea el clúster
```
gcloud container clusters create voteapp-k
```
![k8_1](https://user-images.githubusercontent.com/75556597/187821991-1c6c956f-7a96-40d1-876e-b770d8593b76.png)

#
**Se utiliza la aplicación de ejemplo Vote-App**
Primero, se obtienen los credenciales del cúster
```
gcloud container clusters get-credentials voteapp-k
```
Acto seguido, se clona el repositorio fuente de GitHub
```
git clone https://github.com/jluisalvarez/k8s-vote-app
```
Luego se sigue el procedimiento especificado en el repositorio
```
cd k8s-vote-app/
kubectl apply -f .
cd ..
```
![k8_2](https://user-images.githubusercontent.com/75556597/187822440-5540709e-740c-47a5-88d7-b9a63a74ae99.png)

Posteriormente, se expone el puerto 31000 y se comprueba la dirección en la que se encuentra disponible el servicio
```
kubectl expose deployment vote-app --type=LoadBalancer --port 31000
kubectl get service
```
![k8_3](https://user-images.githubusercontent.com/75556597/187822695-3070d746-027b-4825-b636-5d138a8ba669.png)

Se comprueba su funcionamiento en el navegador

![k8_4](https://user-images.githubusercontent.com/75556597/187823408-902f0a4d-d3af-4ab5-86c2-3d86a9fd4a1b.png)

#
Como pide la práctica, se escala con el comando correspondiente. En este caso se escala el servicio de votos.
```
kubectl scale deployments/vote --replicas=5
```

#
Se actualiza el deplyment de vote con la última versión (etiqueta after) que se encuentra en el repositorio DockerHub
```
kubectl set image deployments/vote vote=dockersamples/examplevotingapp_vote:after
```

