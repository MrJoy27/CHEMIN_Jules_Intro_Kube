1. Configuration générale de PostgreSQL
type: postgresql

version:
  postgresql: "16"

mode: standalone

- type : type de base de données à déployer.
- version.postgresql : version majeure de PostgreSQL.
- mode : mode de fonctionnement du cluster.
  - standalone : création d'un cluster autonome.
  - replica : création d'un cluster répliquant un autre cluster.
  - recovery : restauration d'un cluster à partir d'une source existante.
2. Nombre d'instances
cluster:
  instances: 3

C'est l'un des paramètres les plus importants. CloudNativePG va créer trois instances PostgreSQL :
- Une instance primaire (primary) permettant la lecture et l'écriture.
- Deux instances secondaires (replicas) répliquant les données de l'instance primaire.
Si l'instance primaire tombe en panne, CloudNativePG peut automatiquement promouvoir une instance secondaire en nouvelle instance primaire.

Contrairement à un simple Deployment Kubernetes, les trois instances ne sont donc pas interchangeables : elles ont des rôles différents.
3. Stockage persistant
cluster:
  storage:
    size: 8Gi
    storageClass: ""

- size : taille du volume persistant de chaque instance.
- storageClass : type de stockage utilisé par Kubernetes. Si vide, CloudNativePG s'appuie normalement sur la StorageClass par défaut.
Chaque instance possède son propre PVC (PersistentVolumeClaim).

Tu peux réduire cette valeur pour ton TP, par exemple à 1Gi.
4. Ressources CPU et mémoire
cluster:
  resources: {}

Permet de définir les requests et les limits de chaque instance PostgreSQL.

Par exemple :
cluster:
  resources:
    requests:
      cpu: 250m
      memory: 256Mi
    limits:
      cpu: 500m
      memory: 512Mi

Ces valeurs sont données à titre d'exemple pour un petit déploiement de TP.
5. Initialisation de la base de données
cluster:
  initdb: {}

Permet de configurer la création initiale de la base de données.

Par exemple, pour reprendre la base reviews de ton précédent TP :
cluster:
  initdb:
    database: reviews
    owner: admin

CloudNativePG peut automatiquement générer un Secret Kubernetes contenant les identifiants de connexion.

Il est également possible d'exécuter des commandes SQL lors de l'initialisation :
cluster:
  initdb:
    database: reviews
    owner: admin
    postInitApplicationSQL:
      - CREATE TABLE reviews (id SERIAL PRIMARY KEY, content TEXT);

6. Rolling Update
cluster:
  primaryUpdateMethod: switchover
  primaryUpdateStrategy: unsupervised

Cela rejoint directement ce que tu as étudié précédemment sur les Rolling Updates.

CloudNativePG met d'abord à jour les instances secondaires, puis s'occupe de l'instance primaire.
- switchover : bascule du rôle primaire vers une instance secondaire déjà mise à jour.
- restart : redémarrage de l'instance primaire.
- unsupervised : mise à jour automatique.
- supervised : intervention manuelle nécessaire pour terminer la mise à jour du primaire.
7. Réplication synchrone
cluster:
  postgresql:
    synchronous: {}

Permet de configurer la réplication synchrone entre les instances PostgreSQL.

Par défaut, la réplication est asynchrone.

Avec une réplication synchrone, une transaction peut attendre la confirmation d'une ou plusieurs instances secondaires avant d'être validée.

Cela améliore les garanties de conservation des données, mais peut augmenter la latence des écritures.