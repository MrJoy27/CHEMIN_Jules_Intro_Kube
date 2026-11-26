```bash
kubectl get pods
```

```text
NAME                                          READY   STATUS    RESTARTS   AGE
api-alpha-fd845d97b-k2vcw                     1/1     Running   0          66s
api-alpha-fd845d97b-zv2lp                     1/1     Running   0          66s
api-beta-5df6b7557d-m5ggn                     1/1     Running   0          66s
api-beta-5df6b7557d-z24x6                     1/1     Running   0          66s
```

On remarque que les pods tournent bien. Les deux deploys (alpha et beta) sont liés au même port. Le service est relié à ce même port. Lorsqu'on interroge le service, kube choisit d'interroger au hasard un des deux deploys.

On remarque que seulement alpha répond et que le reste du temps béta ne répond pas. Il y a donc un probleme avec béta. En effet, le service beta n'écoute pas le bon port. Ainsi, il suffit de modifier le port que béta écoute pour que l'on ait bien des réponses des deux deploys.

Attention, il faut bien penser à supprimer les pods des tps précédents. Un autre de mes services s'appelait api ce qui faisait que lorsque je faisais un curl il y avait 3 deploys différents qui pouvait répondre ce qui changeait l'intérêt du debug lab.