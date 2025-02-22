● Lecture02. Helm Masterclass: 50 Practical Demos for Kubernetes DevOps

---------------------
1. Helm 설치
참고1 : https://helm.sh/docs/intro/install/
참고2 : 아래 설치진행시에 에러가 발생할 경우에 아래 명령 실행후에 다시 진행할 것
        $ sudo dpkg --configure -a

```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```