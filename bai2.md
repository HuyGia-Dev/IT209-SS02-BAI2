# Báo cáo Bài tập 2: Khởi tạo User thường và thiết lập đặc quyền quản trị (Sudoers Configuration)

## 1. Các lệnh Linux đã thực thi trên Server

### Bước 1: Khởi tạo user `devops`
```bash
sudo adduser devops
```

### Bước 2: Thêm user `devops` vào nhóm quản trị `sudo`
```bash
sudo usermod -aG sudo devops
```

### Bước 3: Sao chép cấu hình SSH Key từ root sang user `devops`
```bash
sudo rsync --archive --chown=devops:devops ~/.ssh /home/devops/
```

### Bước 4: Phân quyền chính xác cho thư mục `.ssh` và file `authorized_keys`
```bash
sudo chmod 700 /home/devops/.ssh
sudo chmod 600 /home/devops/.ssh/authorized_keys
sudo chown -R devops:devops /home/devops/.ssh
```

---

## 2. Nhật ký (Log) kiểm tra kết quả

### Đăng nhập từ máy cá nhân bằng user `devops`:
```bash
$ ssh -i ~/.ssh/id_rsa devops@159.65.132.18
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.0-88-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

Last login: Sun Oct 15 10:00:00 2023 from 113.161.x.x
devops@ubuntu-s-1vcpu-1gb:~ $
```

### Kiểm tra đặc quyền sudo bằng lệnh `sudo whoami`:
```bash
devops@ubuntu-s-1vcpu-1gb:~ $ sudo whoami
[sudo] password for devops: ********
root
```