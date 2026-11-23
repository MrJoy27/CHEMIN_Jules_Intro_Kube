Quelques difficultés sur la création du StatefulSet: 
il faut penser à allouer suffisament en taille sinon postgre ne se lance pas (j'avais mis 10 mo en pensant que ça suffirait). Aussi il faut vérifier si un autre service n'existe déjà pas

kubectl delete pod postgres-0

kubectl get pods
NAME                                          READY   STATUS    RESTARTS   AGE
postgres-0                                    1/1     Running   0          2m8s

Le service est automatiquement recrée par le pvc