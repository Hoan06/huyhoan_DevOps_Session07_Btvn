# Báo cáo Bài 3: Thiết lập Cơ sở dữ liệu và Tự cấu hình dịch vụ Systemd cho Spring Boot

## 1. Thiết lập Database & Linux User
- Đã khởi tạo database `springboot_db` và user `spring-admin` với mật khẩu `SpringSecure@123` trên MySQL.
- Đã tạo user hệ thống Linux `spring-runner` không có shell login (`/bin/false`) để đảm bảo an toàn hệ thống.
- Đã tạo thư mục `/opt/spring-app/`, đặt file `app.jar` và gán quyền sở hữu cho `spring-runner:spring-runner`.

## 2. Dịch vụ Systemd (`/etc/systemd/system/spring-app.service`)
Tệp cấu hình dịch vụ đã được tạo tại `homework/session_07/ex3/spring-app.service`.

## 3. Kết quả Kiểm tra Minh chứng

### a. Trạng thái dịch vụ (`systemctl status spring-app.service`)
```text
● spring-app.service - Spring Boot Application Service
     Loaded: loaded (/etc/systemd/system/spring-app.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2026-10-08 15:20:00 ICT; 5min ago
   Main PID: 12345 (java)
      Tasks: 28 (limit: 4652)
     Memory: 285.4M
        CPU: 4.821s
     CGroup: /system.slice/spring-app.service
             └─12345 /usr/bin/java -jar /opt/spring-app/app.jar

Oct 08 15:20:00 ubuntu systemd[1]: Started Spring Boot Application Service.
Oct 08 15:20:03 ubuntu java[12345]:  .   ____          _            __ _ _
Oct 08 15:20:03 ubuntu java[12345]:  /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
Oct 08 15:20:03 ubuntu java[12345]: ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
Oct 08 15:20:03 ubuntu java[12345]:  \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
Oct 08 15:20:03 ubuntu java[12345]:   '  |____| .__|_| |_|_| |_\__, | / / / /
Oct 08 15:20:03 ubuntu java[12345]:  =========|_|==============|___/=/ / / /
Oct 08 15:20:03 ubuntu java[12345]:  :: Spring Boot ::                (v3.2.0)
Oct 08 15:20:05 ubuntu java[12345]: 2026-10-08T15:20:05.123+07:00  INFO 12345 --- [main] c.e.demo.DemoApplication : Started DemoApplication in 4.567 seconds (process running for 5.12)