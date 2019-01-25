# clairCT

Please make appropriate changes to the slack.sh file in URL for the webhook
Do start the environment by executing following commands on terminal:

docker run -p 5432:5432 -d --name db arminc/clair-db:2017-10-17
docker run -p 6060:6060 --link db:postgres -d --name clair arminc/clair-local-scan:v2.0.1


Ports could change as per your configuration.
