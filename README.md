#install gcloud

gcloud components install kubectl
gcloud components update

gcloud init
gcloud auth application-default login

gcloud container clusters create test \
  --zone=us-central1-b \
  --machine-type=n1-standard-1 \
  --num-nodes=1 \
  --enable-autorepair \
  --enable-autoupgrade \
  --enable-autoscaling \
  --min-nodes=1 \
  --max-nodes=1

gcloud config set container/cluster test
gcloud container clusters get-credentials test


kubectl apply -f limits.yaml

kubectl apply -f nodejs-deployment.yaml
kubectl apply -f nodejs-service.yaml

kubectl apply -f app-ingress.yaml
