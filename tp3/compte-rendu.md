## Déploiement du service et de l'ingress

IL faut tout d'abord écrire le service.yaml. C'est assez facile en reprenant l'exemple du cours.

On utilise

```bash
kubectl apply -f service.yaml
```

pour initialiser le service.

Le service a bien été crée et est associé à une adresse ip virtuelle.

```bash
kubectl get services
```

```text
NAME                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
mon-api-service       ClusterIP   10.233.22.112   <none>        8000/TCP     15s
```

En faisant

```bash
curl http://mon-api-service:8000/hello
```

```text
"world"
```

On constate alors que le service est bien lancé. On peut faire curl car le service vscode est lui même un pod d'Onyxia. En fait, toute l'architecture d'Onyxia se base sur Kubernetes.

On écrit ensuite le fichier ingress.yaml. Evidemment, il faut faire attention aux ports et à l'url de host.

```bash
kubectl apply -f ingress.yaml
```

L'ingress est bien crée.

```bash
kubectl get ingress
```

```text
NAME                     CLASS    HOSTS                                       ADDRESS   PORTS     AGE
mon-api-ingress          <none>   mon-api-jchemin.lab.sspcloud.fr                       8000       12s
```

En allant sur [mon-api-jchemin.lab.sspcloud.fr/docs](http://mon-api-jchemin.lab.sspcloud.fr/docs) on a accès à la page docs de FastAPI, ce qui prouve bien que le déployement a fonctionné. (voir aussi le fichier api-deployé.png)

---

## Déploiement de l'application 3-tier

Pour l'application 3-tier, j'ai tout mis dans un seul fichier à l'aide de la syntaxe "---" de yaml.

On écrit d'abord les deployments, puis les services, puis les ingress. Ici il n'y a qu'un seul ingress à écrire car on souhaite seulement rendre le frontend accessible aux utilisateurs.

Il faut faire attention aux ports qu'on utilise. IL faut les vérifier sur les images docker hub. J'ai l'impression qu'une bonne pratique peut être de garder les mêmes ports du deployment aux ingress pour ne pas s'embrouiller

Il fallait bien attention aux nom des services. Bien appeler le backend "backend" car le frontend est configuré pour communiquer avec un service appelé comme ceci

```bash
kubectl get deploy
```

```text
NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
backend-3-tier-deployment    3/3     3            3           12m
frontend-3-tier-deployment   3/3     3            3           12m
postgres                     1/1     1            1           12m
```

On constate que les trois deploy sont bien lancés. (voir également le 3-tier-deployé.png pour constater que le frontend est bien déployé.

Pour finir on constate que lorsqu'on redémarre le service postgre, on perd les données. Il n'y a pas de persistance pour l'instant.
