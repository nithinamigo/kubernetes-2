# kubernetes-2
# all these commands are used in macos
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_Darwin_amd64.tar.gz" \
| tar xz -C /tmp

sudo mv /tmp/eksctl /usr/local/bin

eksctl create cluster \
  --name eks-demo \
  --version 1.30 \
  --region ap-south-1 \
  --nodegroup-name ng1 \
  --node-type t3.micro \
  --nodes 1

kubectl apply -f manifests/nginx-deployment.yaml

kubectl apply -f manifests/nginx-service.yaml

kubectl get svc
