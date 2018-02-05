# k8s-1.8-dashboard-heapster-mod

Kusernetes 1.8.x Dashboard(Heapster 포함)을 기반으로 Nodeport 30000를 적용하여 비교적 쉽게 설치/사용하도록 수정

# Prerequisites

* Kubernetes v1.8.x~v1.9.0 이 설치되고 클러스터가 정상 작동 상태여야 함
* Dashboard 가 설치되어 있을 경우 Heapster 와 함께 삭제해야 함

# Usage

**Installation**

* git clone THIS-REPOSITORY & change directory
* cd k8s-1.8.1-dashboard
* kubectl create -f kubernetes-dashboard.yaml
* kubectl create -f kubernetes-dashboard-admin-rbac.yaml
* cd ../
* kubectl create -f k8s-heapster/

**Dashboard access**

* **Check the cluster status by** kubectl get pods -nkube-system -w
* kubectl -n kube-system get secret | grep kubernetes-dashboard-admin
* **Copy token data by** kubectl describe -nkube-system secret kubernetes-dashboard-admin-token-xxxxx
* Or just use single command simply like this ...
kubectl describe -nkube-system secret \`kubectl -n kube-system get secret | grep kubernetes-dashboard-admin | cut -f1 -d" "\`

* Access to https://minion-ip:30000/, select 'Token' button
* **Paste token data**, select 'Sign in' and have fun with k8s dashboard!
