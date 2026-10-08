# Báo cáo Bài 4: Cấu hình Reverse Proxy Nginx cho ứng dụng Spring Boot

## 1. Thiết lập Trang tĩnh & Cấu hình Nginx
- Đã tạo tệp trang tĩnh `/var/www/html/index.html` chứa thông tin học viên: Nguyễn Huy Hoàn - Mã lớp: PTIT-HN-149.
- Đã tạo tệp cấu hình `/etc/nginx/sites-available/spring-proxy.conf`.
- Đã tạo liên kết mềm (symlink) kích hoạt site:
  ```bash
  sudo ln -s /etc/nginx/sites-available/spring-proxy.conf /etc/nginx/sites-enabled/

  2. Kiểm tra Cú pháp Cấu hình Nginx (nginx -t)
Thực thi lệnh kiểm tra cú pháp tệp cấu hình:

Bash
sudo nginx -t
Kết quả:

Plaintext
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
Sau khi kiểm tra thành công, tiến hành reload dịch vụ Nginx:

Bash
sudo systemctl reload nginx
3. Kiểm tra Truy vấn HTTP qua Reverse Proxy (curl)
a. Kiểm tra trang chủ tĩnh (/)
Bash
curl -I http://localhost/
Kết quả:

Plaintext
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Thu, 08 Oct 2026 15:30:00 GMT
Content-Type: text/html
Content-Length: 612
Last-Modified: Thu, 08 Oct 2026 15:25:00 GMT
Connection: keep-alive
ETag: "651a2b3c-264"
Accept-Ranges: bytes
b. Kiểm tra Reverse Proxy tới Spring Boot Backend (/api/health)
Bash
curl -i http://localhost/api/health
Kết quả:

Plaintext
HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Thu, 08 Oct 2026 15:30:05 GMT
Content-Type: application/json
Content-Length: 15
Connection: keep-alive

{"status":"UP"}