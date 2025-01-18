# vtp-crm-infra

# Data Layer : ở mục dev

chạy lệnh sau trong docker tại thư mục dev

```sh
docker-compose up
```

sau khi chạy xong thì :
- kafka : `localhost:9094`
- redis: `localhost:6379` , username đăng nhập: `default` password: `1234`
- postgres: `localhost:5432` username đăng nhập: `postgres` password: `1234`



# ELK stack: ở thư mục elk chạy lệnh docker sau.

chạy lệnh sau để setup thông tin account.

```sh
docker-compose up setup
```
sau khi setup xong thì chạy lệnh: 
```sh
docker-compose up
```

Kibana khoảng một phút để khởi tạo, sau đó truy cập giao diện web Kibana bằng cách mở <http://localhost:5601> trong web
trình duyệt và sử dụng thông tin đăng nhập (mặc định) sau để đăng nhập:

* Người dùng: *elastic*
* Mật khẩu: *changeme*

---
Các bước cài đặt trên môi trường develop/staging 

- Cài docker 
- Cài git  
- Clone project infa về Chạy để có kafka, postgres, redis 
- Cài đặt github self-hosted -> cicd 

# Cài đặt docker  

Để cài đặt Docker trên Ubuntu, bạn có thể thực hiện các bước sau đây: 

**Bước 1: Cập nhật gói phần mềm của hệ thống:** 
```bash 
sudo apt update && sudo apt upgrade
``` 

**Bước 2: Cài đặt các gói tiền điều kiện:** 
```bash 
sudo apt install apt-transport-https ca-certificates curl software-properties-common 
``` 

**Bước 3: Thêm khóa GPG của Docker:** 
```bash 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 
```

**Bước 4: Thêm repository Docker:** 
```bash 
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
``` 

**Bước 5: Cập nhật lại danh sách gói phần mềm và cài đặt Docker:** 
```bash 
sudo apt update 
sudo apt install docker-ce docker-ce-cli containerd.io 
```

 **Bước 6: Kiểm tra quyền truy cập:** 
thêm người dùng của mình vào nhóm "docker" để có quyền truy cập vào socket Docker.  
```bash 
sudo usermod -aG docker $USER 
``` 
Sau đó, đăng nhập lại hoặc mở một phiên làm việc mới để áp dụng thay đổi. 

**Kiểm tra trạng thái Docker daemon:** 
Kiểm tra xem Docker daemon đã được khởi động chưa: 
```bash 
sudo systemctl status docker 
```

Nếu Docker daemon chưa được khởi động, bạn có thể khởi động nó bằng lệnh: 
```bash 
sudo systemctl start docker 
```

Để đảm bảo rằng Docker daemon sẽ tự động khởi động khi hệ thống khởi động, sử dụng lệnh sau: 
```bash 
sudo systemctl enable docker 
``` 

Sau khi thực hiện các bước trên, hãy đăng nhập lại vào hệ thống để áp dụng thay đổi. 

Chú ý rằng quy trình cài đặt Docker có thể thay đổi theo phiên bản cụ thể của Ubuntu hoặc Docker. Luôn kiểm tra tài liệu chính thức để đảm bảo rằng bạn đang sử dụng hướng dẫn đúng với phiên bản bạn đang cài đặt. 

# Cài docker compose: 
Mặc định khi cài đặt Docker, Docker Compose không được cài đặt kèm theo. Docker Compose là một công cụ riêng biệt mà bạn cần phải cài đặt một cách tường minh sau khi cài Docker. 
cách cài đặt Docker Compose: 

**Tải Docker Compose:** 
Chạy lệnh sau để tải phiên bản mới nhất của Docker Compose: 
```bash 
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose 
 ``` 

Nếu bạn gặp vấn đề với lệnh trên, bạn có thể sử dụng phiên bản cụ thể bằng cách thay thế "latest" trong URL bằng phiên bản mong muốn. 
**Cấp quyền thực thi:** 

Cấp quyền thực thi cho tệp tải về: 

```bash 
sudo chmod +x /usr/local/bin/docker-compose 
```

**Kiểm tra cài đặt:** 
Kiểm tra xem Docker Compose đã được cài đặt chưa bằng lệnh: 

```bash 
docker-compose --version 
``` 

Nếu cài đặt thành công, sẽ nhìn thấy phiên bản Docker Compose hiện tại, 
Nếu không thành công hãy restart lại hoặc thoát phiên rồi đăng nhập lại. 

Lệnh reboot:  

```bash  
sudo reboot 
``` 

# Cài đặt git :  

Để cài đặt Git trên Ubuntu, bạn có thể sử dụng trình quản lý gói APT. Dưới đây là các bước cài đặt: 

**Bước 1: Mở Terminal:** 

- Sử dụng tổ hợp phím `Ctrl + Alt + T` để mở Terminal. 

**Bước 2: Cập nhật gói thông tin:** 
- Chạy lệnh sau để cập nhật gói thông tin của trình quản lý gói APT:
- 
```bash 
sudo apt update 
``` 

**Bước 3: Cài đặt Git:** 
- Chạy lệnh sau để cài đặt Git: 

```bash 
sudo apt install git 
``` 

**Bước 4: Kiểm tra phiên bản Git:** 
- Kiểm tra xem Git đã được cài đặt chưa bằng cách chạy lệnh: 

```bash 
git --version 
``` 

- Nếu cài đặt thành công, bạn sẽ nhìn thấy phiên bản Git hiện tại. 

**Bước 5: Clone project: vtp-crm-infra** 

```bash
git clone  
cd vtp-crm-infra ; 
git checkout develop;
git pull;
```

# Cài đặt kafka, redis, postgres: 

```bash
docker-compose -f ~/vtp-crm-infra/dev/docker-compose.yml pull && docker-compose -f ~/vtp-crm-infra/dev/docker-compose.yml up -d 
```

# Cài đặt github selfhosted runner để CICD

tham khảo link: https://github.com/organizations/DSSVN-ViettelPost-CRM/settings/actions/runners/new?arch=x64&os=linux

Định cấu hình ứng dụng github self-hosted runner dưới dạng dịch vụ. 

https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service 

 

 
