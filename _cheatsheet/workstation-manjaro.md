# Workstation - manjaro

## devenv
shellrc

## package

`sudo pacman -Syu`

### docker - container
```
sudo pacman -S --noconfirm docker docker-compose docker-machine
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
```

#### virtualbox & vagrant
https://wiki.archlinux.org/index.php/Vagrant
```
sudo pacman -S --noconfirm virtualbox vagrant
vagrant plugin install vagrant-vbguest vagrant-share
```

#### kubernetes, minikube, microk8s
https://microk8s.io/
https://kubernetes.io/ko/docs/tasks/tools/install-minikube/

minikube 1번방법
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
minikube 2번방법
```
yaourt minikube
```
minikube 3번방법
http://blog.programmableproduction.com/2018/03/08/Archlinux-Setup-Minikube-using-KVM/


