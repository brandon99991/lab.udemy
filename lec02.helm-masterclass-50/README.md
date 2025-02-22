● Lecture02. Helm Masterclass: 50 Practical Demos for Kubernetes DevOps

https://github.com/stacksimplify/helm-masterclass

---------------------
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


helm list


helm uninstall


```
