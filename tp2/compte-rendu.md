# COMPTE-RENDU TP2

Il faut bien écrire le fichier deployment.yaml. Je suis reparti de l'exemple donné dans le cours. Il suffit de modifier le nom du docker ainsi que mon pseudo Docker Hub.

Ensuite, pour déployer, il faut faire :

```bash
kubectl apply -f deployment.yaml
```

Dans la commande, `-f` veut dire filename.

On peut ensuite vérifier les Deployments avec :

```bash
kubectl get deployments
```

Ceci nous est renvoyé. 3 replicas ont bien été créés :

```text
NAME                 READY   UP-TO-DATE   AVAILABLE   AGE
mon-api-deployment   3/3     3            3           21s
```

On peut ensuite vérifier les Pods en faisant :

```bash
kubectl get pods
```

```text
NAME                                 READY   STATUS    RESTARTS   AGE
mon-api-deployment-b8d4dcf9b-dxbtm   1/1     Running   0          41s
mon-api-deployment-b8d4dcf9b-p45hc   1/1     Running   0          41s
mon-api-deployment-b8d4dcf9b-pfnz5   1/1     Running   0          41s
```

On remarque que les trois Pods sont bien lancés.

Pour tester sans créer de Service, on peut utiliser par exemple :

```bash
kubectl port-forward deployment/mon-api-deployment 8000:8000
```

Puis interroger l'API avec `curl` :

```bash
curl http://localhost:8000/hello
```

> **ATTENTION :** Il faut penser à se mettre en administrateur Kubernetes lorsqu'on lance le service Onyxia.
