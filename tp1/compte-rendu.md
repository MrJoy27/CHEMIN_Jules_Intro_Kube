# PARTIE PYTHON

### Q2)

On crée d'abord un Dockerfile. Le Dockerfile est assez petit. Il faut penser à installer les requirements et à bien initialiser les ports.

### Q4)

Pour build l'image Docker, on utilise la commande :

```
sudo docker build -t mon-api .
```



Il faut bien penser à se mettre en sudo pour utiliser Docker. Le téléchargement des images peut prendre un peu de temps la première fois qu'on charge un Dockerfile (forcément il faut installer Python ou Java).

### Q5)

Pour lancer l'image, on utilise :

```
sudo docker run -p 8000:8000 mon-api
```



On peut bien faire une requête à l'aide du endpoint /docs fourni par FastAPI ou à l'aide de curl :

```
curl http://localhost:8080/hello
```

L'API nous renvoie bien "world" lorsqu'on interroge /hello\.

### Q6)
On utilise docker log pour consulter les logs de l'image docker.

```
sudo docker logs "nom de l'image"
```
Pour retrouver le nom de l'image faire :
```
sudo docker -ps
```


### Q8)

On doit d'abord se connecter avec un compte Docker en utilisant \:

```
sudo docker login -u mrjoy27
```



Puis en renseignant le mot de passe.

Il faut penser à modifier le nom de notre image pour qu'elle convienne à Docker Hub \:

```
sudo docker tag mon-api mrjoy27/mon-api:1.0
```



Ensuite, on peut push (cela peut prendre un peu de temps).

```
sudo docker push mrjoy27/mon-api:1.0
```



---

# PARTIE JAVA

Globalement, c'est la même procédure que dans la partie Python.

J'ai d'abord eu un problème lors de mon premier docker build où VSCode a crash durant le téléchargement de l'image Maven Temurin. Une fois ce crash, je n'arrivais plus à charger l'image. Je suppose a posteriori que c'était parce que l'image téléchargée était corrompue.

J'ai donc utilisé l'image Java Amazon Corretto  qui fonctionnait très bien.

Sur l'écriture du Dockerfile, j'ai l'impression qu'une bonne approche est de se demander comment je lancerais l'application dans la vraie vie et globalement ça suffit pour le construire.

Ensuite on build l'image, on l'a run puis on peut l'uploader sur Docker hub.