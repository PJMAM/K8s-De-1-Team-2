# Topic : Tìm hiểu K8s Và đề mô áp dụng

# Thành viên
- Nguyễn Duy Phước - 19133003
- Lưu Gia Bảo      - 19133008
- Nguyễn Quốc Việt - 19133068

# Thông Tin về k8s
- [Kubernate](https://kubernetes.io/vi/docs/concepts/overview/what-is-kubernetes/)
- [MiniKube](https://viblo.asia/p/tim-hieu-co-ban-ve-kubernetes-k8s-part-2-minikube-XL6lA2Mp5ek)

# Cài đặt kubernetes với MiniKube trên Ubuntu AWS Ec2 Instance 

### MiniKube 

- MiniKube được sử dụng để chạy Kubernetes cục bộ.

- Minikube là một cụm Kubernetes một nút mà bạn có thể sử dụng cục bộ trong máy của riêng mình để kiểm tra các tập lệnh triển khai Kubernetes của bạn, khám phá và nghiên cứu Kubernetes, v.v.

- MiniKube được sử dụng cho Mục đích Phát triển.

- Minikube không thể được sử dụng trong Sản xuất.


### Các bước cài đặt

#### Bước 1 Cài đặt Docker 

```sh

sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 
 sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io

````

#### Bước 2 Cài đặt KubeCtl 

```sh
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin/kubectl

kubectl version

```

#### Bước 3 Cài đặt MiniKube
```sh

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

chmod +x ./minikube

sudo mv ./minikube /usr/local/bin/minikube

sudo apt-get install conntrack  // this is dependecy for minicube 
```

#### Bước 4 Chạy MiniKube

```sh

minikube start --vm-driver=none  // 

```

#### Bước 5 Kiểm tra 

```sh

kubectl get node 

```


### Triển khai mongodb 

#### Khi đã tạo được cụm kubernetes thì chạy các lệnh sau để triển khai mongodb 
```
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f mongo-configmap.yaml 
kubectl apply -f mongo-express.yaml
```
#### Kiểm tra các thành phần đang chạy 
```
kubectl get all
```
#### Để truy cập được lên web dùng địa chỉ ip máy của máy mình  với port 30000
	VD : http://34.193.147.254:30000/