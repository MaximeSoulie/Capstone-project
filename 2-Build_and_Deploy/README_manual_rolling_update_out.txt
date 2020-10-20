Here is how I performed the Rolling Update manually via CLI on the Jenkins build server

ubuntu@ip-172-31-46-99:~$ kubectl get pods -n mlapp4ms
NAME                                     READY   STATUS    RESTARTS   AGE
mycapstoneapp-service-57dd6556cc-9xwdz   1/1     Running   0          76m
mycapstoneapp-service-57dd6556cc-jv29w   1/1     Running   0          76m
mycapstoneapp-service-57dd6556cc-mm7w6   1/1     Running   0          76m


ubuntu@ip-172-31-46-99:~$ kubectl scale --replicas=0 rs/mycapstoneapp-service-57dd6556cc -n mlapp4ms
replicaset.apps/mycapstoneapp-service-57dd6556cc scaled


ubuntu@ip-172-31-46-99:~$ kubectl get pods -n mlapp4ms
NAME                                     READY   STATUS              RESTARTS   AGE
mycapstoneapp-service-57dd6556cc-9xwdz   1/1     Terminating         0          76m
mycapstoneapp-service-57dd6556cc-br6ms   0/1     ContainerCreating   0          6s
mycapstoneapp-service-57dd6556cc-jv29w   1/1     Terminating         0          76m
mycapstoneapp-service-57dd6556cc-kdj6w   0/1     ContainerCreating   0          6s
mycapstoneapp-service-57dd6556cc-mm7w6   1/1     Terminating         0          76m
mycapstoneapp-service-57dd6556cc-x7nbp   0/1     ContainerCreating   0          6s


ubuntu@ip-172-31-46-99:~$ kubectl get pods -n mlapp4ms
NAME                                     READY   STATUS        RESTARTS   AGE
mycapstoneapp-service-57dd6556cc-9xwdz   1/1     Terminating   0          77m
mycapstoneapp-service-57dd6556cc-br6ms   1/1     Running       0          33s
mycapstoneapp-service-57dd6556cc-jv29w   1/1     Terminating   0          77m
mycapstoneapp-service-57dd6556cc-kdj6w   1/1     Running       0          33s
mycapstoneapp-service-57dd6556cc-mm7w6   1/1     Terminating   0          77m
mycapstoneapp-service-57dd6556cc-x7nbp   1/1     Running       0          33s

ubuntu@ip-172-31-46-99:~$ kubectl rollout status deployment.v1.apps/mycapstoneapp-service -n mlapp4ms
Waiting for deployment "mycapstoneapp-service" rollout to finish: 0 of 3 updated replicas are available...
Waiting for deployment "mycapstoneapp-service" rollout to finish: 2 of 3 updated replicas are available...
deployment "mycapstoneapp-service" successfully rolled out

ubuntu@ip-172-31-46-99:~$ kubectl rollout status deployment.v1.apps/mycapstoneapp-service -n mlapp4ms
deployment "mycapstoneapp-service" successfully rolled out
