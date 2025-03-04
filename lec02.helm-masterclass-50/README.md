

● 현재 진행 사항  
  12-Helm-Dev-Basics  (완료 / 2025.03.03)



● Lecture02. Helm Masterclass: 50 Practical Demos for Kubernetes DevOps

https://github.com/stacksimplify/helm-masterclass  

https://github.com/stacksimplify/helm-charts  
    
https://stacksimplify.github.io/helm-charts/



1. Helm 설치
설치 안내 : https://helm.sh/docs/intro/install/

```
# 참고 : 아래 설치진행시에 에러가 발생할 경우에 아래 명령 실행후에 다시 진행할 것
        $ sudo dpkg --configure -a

curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

2. Helm 기본 명령어
```
# Helm Version 확인
$ helm version

# Helm 환경변수 확인
$ helm env

# Helm repository 목록
$ helm repo list

# Helm repository 추가
// helm repo add <DESIRED-NAME> <HELM-REPO-URL>
$ helm repo add mybitnami https://charts.bitnami.com/bitnami

# Helm repository에서 찾기
// helm search repo <KEY-WORD>
$ helm search repo nginx
$ helm search repo

# Helm repository에서 keyword에 해당 하는 모든 버젼 찾기
$ helm search repo wildfly --versions

# Helm repository에서 keyword에 해당 하는 특정 버젼 찾기
$ helm search repo wildfly --version 13.3.10

# Helm repository update 하기
$ helm repo update

# Install Helm Chart
// helm install <RELEASE-NAME> <repo_name_in_your_local_desktop/chart_name>
$ helm install mynginx mybitnami/nginx

# Helm Chart 배포 목록
$ helm list
$ helm ls
$ helm list --output=yaml
$ helm list --output=json
$ helm list -o json
$ helm list -o yaml
$ helm list --namespace=dev
$ helm list --namespace=default
$ helm list -n dev
$ helm list -n default

# Helm Chart 배포 삭제 / k8s에서 리소스 삭제됨.
$ helm uninstall mynginx


---------------------------------------

# Add Helm Repository
$ helm repo add stacksimplify https://stacksimplify.github.io/helm-charts/

# Search Helm Repository
$ helm search repo mychart1
$ helm search repo mychart1 --versions
$ helm search repo mychart2 --versions

# Install myapp1 Helm Chart
$ helm install myapp1 stacksimplify/mychart1 

// chart의 values.yaml에서 image tag값이 비었을 경우에는 
// Chart.yaml의 appVersion의 값으로 채워진다.  
// 예) tag: ""
// 이 예에서는 Chart.yaml에서 아래와 같이 되어 있으므로  
// 이미지 tag는 1.0.0이 된다.
// 예) appVersion: "1.0.0"1.0.0.

# Review the Docker Image Versions we are using
https://github.com/users/stacksimplify/packages/container/package/kubenginx
Image Tags: 1.0.0, 2.0.0, 3.0.0, 4.0.0

# Helm image Upgrade
// helm upgrade <RELEASE-NAME> <repo_name_in_your_local_desktop/chart_name> --set <OVERRIDE-VALUE-FROM-values.yaml>
$ helm upgrade myapp1 stacksimplify/mychart1 --set "image.tag=2.0.0"

# Additional List commands
helm list --superseded
helm list --deployed

$ helm upgrade myapp1 stacksimplify/mychart1 --set "image.tag=3.0.0"

$ helm upgrade myapp1 stacksimplify/mychart1 --set "image.tag=4.0.0"


# Helm replica Upgrade
$ helm upgrade myapp1 stacksimplify/mychart1 --set "replicaCount=4"

# helm history
//helm history RELEASE_NAME
$ helm history myapp1


# helm status
$ helm status myapp1
$ helm status myapp1 --show-desc
$ helm status myapp1 --show-resources
$ helm status myapp1 --revision 2

# helm uninstall
$ helm uninstall myapp1

-----------------------------------------

# Search Helm Repo
$ helm search repo mychart2

# Search Helm Repo with --versions
$ helm search repo mychart2 --versions

# Search Helm Repo with --version
//helm search repo mychart2 --version "CHART-VERSIONS"
$ helm search repo mychart2 --version "0.2.0"

# Install Helm Chart by specifying Chart Version
//helm install myapp101 stacksimplify/mychart2 --version "CHART-VERSION"
$ helm install myapp101 stacksimplify/mychart2 --version "0.1.0"

# List Kubernetes Resources Deployed as part of this Helm Release
$ helm status myapp101 --show-resources

# Helm Upgrade using Chart Version
$ helm upgrade myapp101 stacksimplify/mychart2 --version "0.2.0"

# List Kubernetes Resources Deployed as part of this Helm Release
$ helm status myapp101 --show-resources

# List Release History
$ helm history myapp101

# Helm Upgrade using Chart Version
$ helm upgrade myapp101 stacksimplify/mychart2

# List Kubernetes Resources Deployed as part of this Helm Release
$ helm status myapp101 --show-resources

# List Release History
$ helm history myapp101

# Rollback to previous version
$ helm rollback myapp101

# List Kubernetes Resources Deployed as part of this Helm Release
$ helm status myapp101 --show-resources

# List Release History
$ helm history myapp101

# Rollback to previous version
//helm rollback RELEASE-NAME REVISION
$ helm rollback myapp101 1

# List Kubernetes Resources Deployed as part of this Helm Release
$ helm status myapp101 --show-resources

# List Release History
$ helm history myapp101

# List Helm Releases
$ helm list
$ helm list --superseded
$ helm list --deployed

# Uninstall Helm Release with --keep-history Flag
// helm uninstall <RELEASE-NAME> --keep-history
$ helm uninstall myapp101 --keep-history

# List Helm Releases which are uninstalled
$ helm list --uninstalled

# helm status command
$ helm status myapp101

# Rollback Helm Uninstalled Release
//helm rollback <RELEASE> [REVISION] [flags]
$ helm rollback myapp101 3

---------------------------------------------------

# Install helm with --generate-name flag
//helm install <repo_name_in_your_local_desktop/chart_name> --generate-name
$ helm install stacksimplify/mychart1 --generate-name

# List Helm Releases
$ helm list
$ helm list --output=yaml

# Helm Status
$ helm status mychart1-1689683948 
$ helm status mychart1-1689683948 --show-resources

# Helm atomic
$ helm install dev101 stacksimplify/mychart1
$ helm install qa101 stacksimplify/mychart1 --atomic

# Install Helm Release by creating Kubernetes Namespace
// --create-namespace는 namespace가 없을 경우에 생성하는 옵션임.
$ helm install dev101 stacksimplify/mychart2 --version "0.1.0" --namespace dev --create-namespace 

# List Helm Release
$ helm list -n dev
$ helm list --namespace dev

# Helm Status
$ helm status dev101 --show-resources -n dev
$ helm status dev101 --show-resources --namespace dev


```
