kubectl get pods
NAME                                          READY   STATUS    RESTARTS   AGE
api-alpha-fd845d97b-k2vcw                     1/1     Running   0          66s
api-alpha-fd845d97b-zv2lp                     1/1     Running   0          66s
api-beta-5df6b7557d-m5ggn                     1/1     Running   0          66s
api-beta-5df6b7557d-z24x6                     1/1     Running   0          66s

les curls ne fonctionnent pas avec le deploiement Beta 

Il suffit de changer les ports de beta qui n'ecoutait pas le bon