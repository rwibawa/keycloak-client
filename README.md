# keycloak-client

## 1. Links:
* [https://www.baeldung.com/spring-boot-keycloak](https://www.baeldung.com/spring-boot-keycloak).

## 2. Install Keycloak in kubernetes with helm charts
```bash
$ helm install stable/keycloak
NAME:   killer-liger
LAST DEPLOYED: Thu Dec 20 23:52:48 2018
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/Service
NAME                           TYPE       CLUSTER-IP     EXTERNAL-IP  PORT(S)  AGE
killer-liger-keycloa-headless  ClusterIP  None           <none>       80/TCP   0s
killer-liger-keycloa-http      ClusterIP  10.98.209.156  <none>       80/TCP   0s

==> v1/StatefulSet
NAME                  DESIRED  CURRENT  AGE
killer-liger-keycloa  1        1        0s

==> v1/Pod(related)
NAME                    READY  STATUS             RESTARTS  AGE
killer-liger-keycloa-0  0/1    ContainerCreating  0         0s

==> v1/Secret
NAME                       TYPE    DATA  AGE
killer-liger-keycloa-db    Opaque  1     0s
killer-liger-keycloa-http  Opaque  1     0s

==> v1/ConfigMap
NAME                       DATA  AGE
killer-liger-keycloa       2     0s
killer-liger-keycloa-test  1     0s


NOTES:

Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  killer-liger-keycloa-http.default.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

$  export POD_NAME=$(kubectl get pods --namespace default -l app=keycloak,release=killer-liger -o jsonpath="{.items[0].metadata.name}")
$  echo "Visit http://127.0.0.1:8080 to use Keycloak"
$  kubectl port-forward --namespace default $POD_NAME 8080

Login with the following credentials:
Username: keycloak
Password: Aq6eO2J2M0

To retrieve the initial user password run:
$ kubectl get secret --namespace default killer-liger-keycloa-http -o jsonpath="{.data.password}" | base64 --decode; echo
```

## 3. Open the admin console.
```bash
$ kubectl port-forward --namespace default killer-liger-keycloa-0 9090:8080
```
[http://localhost:9090](http://localhost:9090).

### 3.1. Create Realm.
### 3.2. Create Client.
### 3.3. Create User.
### 3.4. Create Role.

## 4. Get token.
```bash
curl -X POST \
  http://localhost:9090/auth/realms/SpringBootKeycloak/protocol/openid-connect/token \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=password&client_id=login-app&username=user1&password=Ch%40ng3M3!'
  
curl -X POST \
  http://localhost:9090/auth/realms/SpringBootKeycloak/protocol/openid-connect/token \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'grant_type=refresh_token&client_id=login-app&refresh_token=eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJjNThjMmU4MC04OWExLTQyNmEtYTA1Mi01MDdhMDEyMDU2ZDQifQ.eyJqdGkiOiJmM2NjMTkzMC02MWY4LTRiODEtOTA0My1jZDUzM2UyZjk1Y2MiLCJleHAiOjE1NTE2ODA2NDEsIm5iZiI6MCwiaWF0IjoxNTUxNjc4ODQxLCJpc3MiOiJodHRwOi8vbG9jYWxob3N0OjkwOTAvYXV0aC9yZWFsbXMvU3ByaW5nQm9vdEtleWNsb2FrIiwiYXVkIjoibG9naW4tYXBwIiwic3ViIjoiNDAwZDM5ODMtYTNiYy00NzRmLTkwMDMtYTE1YjQ3YjE2YzcxIiwidHlwIjoiUmVmcmVzaCIsImF6cCI6ImxvZ2luLWFwcCIsImF1dGhfdGltZSI6MCwic2Vzc2lvbl9zdGF0ZSI6ImQ3MTEwMmRhLTNmNzktNDVlYS04YjQ0LWY0ZWEwYzViODM3MCIsInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsInVtYV9hdXRob3JpemF0aW9uIiwidXNlciJdfSwicmVzb3VyY2VfYWNjZXNzIjp7ImFjY291bnQiOnsicm9sZXMiOlsibWFuYWdlLWFjY291bnQiLCJtYW5hZ2UtYWNjb3VudC1saW5rcyIsInZpZXctcHJvZmlsZSJdfX0sInNjb3BlIjoiZW1haWwgcHJvZmlsZSJ9.-xjO76SFlCPqwumKXPfgstnfgCc4zcq1_sDpWikmfd0'
```

## 5. Creating a Spring Boot Application.
[Spring Boot Keycloak Starter](https://search.maven.org/classic/#search%7Cga%7C1%7Ca%3A%22keycloak-spring-boot-starter%22).
