`gcloud config set compute/zone asia-southeast2`

`git clone https://github.com/GoogleCloudPlatform/continuous-deployment-on-kubernetes.git`

`cd continuous-deployment-on-kubernetes`

`gcloud container clusters create jenkins-cd \
  --machine-type n1-standard-2 --num-nodes 2 \
  --scopes "https://www.googleapis.com/auth/source.read_write,cloud-platform" \
  --cluster-version 1.15`
  
 `gcloud container clusters list`
 
 `kubectl cluster-info`
 
 `wget https://get.helm.sh/helm-v3.2.1-linux-amd64.tar.gz`
 
 `tar zxfv helm-v3.2.1-linux-amd64.tar.gz`
 
 `cp linux-amd64/helm .`
 
 `kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin \
        --user=$(gcloud config get-value account)`
        
 `./helm repo add jenkinsci https://charts.jenkins.io`
 
 `./helm repo update`
 
 `./helm version`
 
 `./helm install cd-jenkins -f jenkins/values.yaml jenkinsci/jenkins --version 2.6.4 --wait`
 
 `kubectl get pods`
 
 `export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/component=jenkins-master" -l "app.kubernetes.io/instance=cd-jenkins" -o jsonpath="{.items[0].metadata.name}")
kubectl port-forward $POD_NAME 8080:8080 >> /dev/null &`

`kubectl get svc`

`printf $(kubectl get secret cd-jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo`

Web Preview on port 8080
