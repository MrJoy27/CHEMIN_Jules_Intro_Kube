kubectl get pods
NAME                                          READY   STATUS    RESTARTS   AGE
backend-3-tier-deployment-65cff65474-9b4gs    1/1     Running   0          151m
backend-3-tier-deployment-65cff65474-q4nkd    1/1     Running   0          151m
backend-3-tier-deployment-65cff65474-zrq89    1/1     Running   0          151m
frontend-3-tier-deployment-579fcf8556-7vhgq   1/1     Running   0          151m
frontend-3-tier-deployment-579fcf8556-d8n47   1/1     Running   0          151m
frontend-3-tier-deployment-579fcf8556-zclnw   1/1     Running   0          151m
mon-api-deployment-6dfbccdfcf-9rgz7           1/1     Running   0          106s
mon-api-deployment-6dfbccdfcf-k5bdr           1/1     Running   0          106s
mon-api-deployment-6dfbccdfcf-m4lxs           1/1     Running   0          106s
il faut remarque que restarts=0

kubectl logs mon-api-deployment-6dfbccdfcf-9rgz7
INFO:     Started server process [1]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
INFO:     192.168.253.173:44526 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:52960 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:52966 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:39458 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:39466 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:39476 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:57884 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:57890 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:57904 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:40560 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:40574 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:40590 - "GET /health HTTP/1.1" 200 OK
INFO:     192.168.253.173:41466 - "GET /health HTTP/1.1" 200 OK
Liveness ; redémarrage
readiness: on ne recoit plus de requetes
Liveness est a 10s pour laisser le temps à l'appli de démarrer

===

kubectl apply -f deployment.yaml
deployment.apps/mon-api-deployment configured

kubectl rollout status deployment/mon-api-deployment
Waiting for deployment "mon-api-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "mon-api-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "mon-api-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "mon-api-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "mon-api-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "mon-api-deployment" rollout to finish: 1 old replicas are pending termination...
deployment "mon-api-deployment" successfully rolled out

kubectl get pods -w
NAME                                          READY   STATUS    RESTARTS   AGE
backend-3-tier-deployment-65cff65474-9b4gs    1/1     Running   0          4h18m
backend-3-tier-deployment-65cff65474-q4nkd    1/1     Running   0          4h18m
backend-3-tier-deployment-65cff65474-zrq89    1/1     Running   0          4h18m
frontend-3-tier-deployment-579fcf8556-7vhgq   1/1     Running   0          4h18m
frontend-3-tier-deployment-579fcf8556-d8n47   1/1     Running   0          4h18m
frontend-3-tier-deployment-579fcf8556-zclnw   1/1     Running   0          4h18m
mon-api-deployment-6dfbccdfcf-9rgz7           1/1     Running   0          108m
mon-api-deployment-6dfbccdfcf-k5bdr           1/1     Running   0          108m
mon-api-deployment-6dfbccdfcf-m4lxs           1/1     Running   0          108m
postgres-0                                    1/1     Running   0          4h18m
vscode-python-546216-0                        1/1     Running   0          5h18m
mon-api-deployment-59c5bf85d6-lmkjs           0/1     Pending   0          0s
mon-api-deployment-59c5bf85d6-lmkjs           0/1     Pending   0          0s
mon-api-deployment-59c5bf85d6-lmkjs           0/1     ContainerCreating   0          0s
mon-api-deployment-59c5bf85d6-lmkjs           0/1     ContainerCreating   0          2s
mon-api-deployment-59c5bf85d6-lmkjs           0/1     Running             0          19s
mon-api-deployment-59c5bf85d6-lmkjs           1/1     Running             0          24s
mon-api-deployment-6dfbccdfcf-k5bdr           1/1     Terminating         0          109m
mon-api-deployment-6dfbccdfcf-k5bdr           1/1     Terminating         0          109m
mon-api-deployment-59c5bf85d6-s6gkv           0/1     Pending             0          0s
mon-api-deployment-59c5bf85d6-s6gkv           0/1     Pending             0          0s
mon-api-deployment-59c5bf85d6-s6gkv           0/1     ContainerCreating   0          0s
mon-api-deployment-59c5bf85d6-s6gkv           0/1     ContainerCreating   0          1s
mon-api-deployment-6dfbccdfcf-k5bdr           0/1     Completed           0          110m
mon-api-deployment-6dfbccdfcf-k5bdr           0/1     Completed           0          110m
mon-api-deployment-6dfbccdfcf-k5bdr           0/1     Completed           0          110m
mon-api-deployment-59c5bf85d6-s6gkv           0/1     Running             0          3s
mon-api-deployment-59c5bf85d6-s6gkv           1/1     Running             0          9s
mon-api-deployment-6dfbccdfcf-9rgz7           1/1     Terminating         0          110m
mon-api-deployment-6dfbccdfcf-9rgz7           1/1     Terminating         0          110m
mon-api-deployment-59c5bf85d6-25sjn           0/1     Pending             0          0s
mon-api-deployment-59c5bf85d6-25sjn           0/1     Pending             0          0s
mon-api-deployment-59c5bf85d6-25sjn           0/1     ContainerCreating   0          0s
mon-api-deployment-6dfbccdfcf-9rgz7           0/1     Completed           0          110m
mon-api-deployment-59c5bf85d6-25sjn           0/1     ContainerCreating   0          1s
mon-api-deployment-6dfbccdfcf-9rgz7           0/1     Completed           0          110m
mon-api-deployment-6dfbccdfcf-9rgz7           0/1     Completed           0          110m
mon-api-deployment-59c5bf85d6-25sjn           0/1     Running             0          2s
mon-api-deployment-59c5bf85d6-25sjn           1/1     Running             0          7s
mon-api-deployment-6dfbccdfcf-m4lxs           1/1     Terminating         0          110m
mon-api-deployment-6dfbccdfcf-m4lxs           1/1     Terminating         0          110m
mon-api-deployment-6dfbccdfcf-m4lxs           0/1     Completed           0          110m
mon-api-deployment-6dfbccdfcf-m4lxs           0/1     Completed           0          110m
mon-api-deployment-6dfbccdfcf-m4lxs           0/1     Completed           0          110m