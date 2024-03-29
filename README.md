# configserver


organization


http://localhost:8072/organization/v1/organization/e6a625cc-718b-48c2-ac76-1dfdff9a531e



http://localhost:8072/license/v1/organization/e839ee96-28de-4f67-bb79-870ca89743a0/license/279709ff-e6d5-4a54-8b55-a5c37542025b

docker exec -it postgres bash
\l
\c postgres
\dt



./kcadm.sh config credentials --server http://localhost:8080 --realm master --user admin --password admin  
Logging into http://localhost:8080 as user admin of realm master
bash-5.1$ ./kcadm.sh create realms -s realm=spmia-realm -s enabled=true



docker-compose  up database keycloak

docker exec -it ostock-keycloak bash

cd /opt/keycloak/bin


./kcadm.sh config credentials \
--server http://localhost:8080 \
--realm master \
--user admin \
--password admin


./kcadm.sh create realms -s realm=spmia-realm -s enabled=true

./kcadm.sh create roles -r spmia-realm -s name=ADMIN
./kcadm.sh create roles -r spmia-realm -s name=USER

./kcadm.sh create users -r spmia-realm \
-s username=isabelle \
-s firstName=Isabelle \
-s lastName=Dahl \
-s enabled=true

./kcadm.sh add-roles -r spmia-realm \
--uusername isabelle \
--rolename ADMIN \
--rolename USER

./kcadm.sh create users -r spmia-realm \
-s username=bjorn \
-s firstName=Bjorn \
-s lastName=Vinterberg \
-s enabled=true

./kcadm.sh add-roles -r spmia-realm \
--uusername bjorn \
--rolename USER



./kcadm.sh set-password -r spmia-realm \
--username isabelle --new-password password

./kcadm.sh set-password -r spmia-realm \
--username bjorn --new-password password





curl \
  -d "client_id=ostock" \
  -d "username=isabelle" \
  -d "password=password" \
  -d "grant_type=password" \
  "http://localhost:8080/realms/spmia-realm/protocol/openid-connect/token"
  
  
  
  curl -i http://localhost:8080/admin \
   -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJCcElyY2FyeGNzNG5xVWp4N0djM2xqMmJiaWNNOEhST3dCWVRWcW9hNFlRIn0.eyJleHAiOjE3MDc2NDEzNzAsImlhdCI6MTcwNzY0MTA3MCwianRpIjoiZmEyMzFkZmQtYTg3YS00ZmY0LTk1M2QtYTU1YmMzN2FjYzM5IiwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDo4MDgwL3JlYWxtcy9zcG1pYS1yZWFsbSIsImF1ZCI6ImFjY291bnQiLCJzdWIiOiI3MTRiMTYxYS01NmQyLTQyMTctOGRkNi00MjQwNzYyNjJlZmUiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJvc3RvY2siLCJzZXNzaW9uX3N0YXRlIjoiMWYxMTdjMmItMzViNi00MmI0LTlmNmYtYTI4YmY2NTM3NmNjIiwiYWNyIjoiMSIsImFsbG93ZWQtb3JpZ2lucyI6WyIqIl0sInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyIsImRlZmF1bHQtcm9sZXMtc3BtaWEtcmVhbG0iLCJ1bWFfYXV0aG9yaXphdGlvbiIsIkFETUlOIiwiVVNFUiJdfSwicmVzb3VyY2VfYWNjZXNzIjp7ImFjY291bnQiOnsicm9sZXMiOlsibWFuYWdlLWFjY291bnQiLCJtYW5hZ2UtYWNjb3VudC1saW5rcyIsInZpZXctcHJvZmlsZSJdfX0sInNjb3BlIjoiZW1haWwgcHJvZmlsZSIsInNpZCI6IjFmMTE3YzJiLTM1YjYtNDJiNC05ZjZmLWEyOGJmNjUzNzZjYyIsImVtYWlsX3ZlcmlmaWVkIjpmYWxzZSwibmFtZSI6IklzYWJlbGxlIERhaGwiLCJwcmVmZXJyZWRfdXNlcm5hbWUiOiJpc2FiZWxsZSIsImdpdmVuX25hbWUiOiJJc2FiZWxsZSIsImZhbWlseV9uYW1lIjoiRGFobCJ9.NdCsl5sXOqiAK1qIQS435mQ3uNQkDLgKEneKiwsaWBVKNE7rn38jGtBajRO99Xu6H4uZnEuOGTgh6JW0RjWLnhCVkmk11hIsjcw-PpmPLEvuNzwDQQASw-TEHuJmB8jc1VVRfoa_jHAZBYP2MpuN36zR7Ht30FLLeg8XzdadnvYh780Pr-gGFSuG7s8bVagPOO1RAISmcle2gVar4pSnPHr1QwOJ7SBFVAtKLaM9wiUz-LeTKV7iP_j6CCGBnLYUDecJUfHHgieC0_DeaImXdGxMoEqRydKJExQ-u3HOCoNyygL5V5_vu0CdKW2TFO5EpNNNGbssCaoNjJmRB1-4oQ"
  
