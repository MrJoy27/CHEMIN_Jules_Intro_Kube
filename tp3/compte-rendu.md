
kubectl apply -f service.yaml

kubectl get services
NAME                  TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
mon-api-service       ClusterIP   10.233.22.112   <none>        80/TCP     15s
vscode-python-20690   ClusterIP   None            <none>        8080/TCP   17h
vscode-python-65625   ClusterIP   None            <none>        8080/TCP   18h

kubectl run test-curl1 --image=curlimages/curl --restart=Never --rm -it -- curl http://mon-api-service:8000/hello
"world"

Problématique des pods

Non en fait, curl http://mon-api-service:8000/hello 
"world" suffit car vscode est déjà un curl 


kubectl get ingress
NAME                     CLASS    HOSTS                                       ADDRESS   PORTS     AGE
mon-api-ingress          <none>   mon-api-jchemin.lab.sspcloud.fr                       80        12s
vscode-python-20690-ui   onyxia   user-jchemin-20690-0.user.lab.sspcloud.fr             80, 443   18h
vscode-python-65625-ui   onyxia   user-jchemin-65625-0.user.lab.sspcloud.fr             80, 443   18h
================
Un seul fichier pour le 3-tier 
Faire attention aux ports sur lesquels on déploie (vérifier sur docker hub)
Attention aux noms des services: backend pour que ça fonctionne bien

kubectl get deployments
NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
backend-3-tier-deployment    3/3     3            3           12m
frontend-3-tier-deployment   3/3     3            3           12m
mon-api-deployment           3/3     3            3           18h
postgres                     1/1     1            1           12m