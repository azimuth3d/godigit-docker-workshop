พื้นฐานการใช้งาน docker-compose
docker compose ขอเขียนอยู่ในรูปแบบของ .yaml โดยใช้ชื่อ key แล้ว Indentation ในกำหนดค่า

```yaml
version: 3.0
    services:
       ชื่อ service:
         image: godigit/xxx
         build: ./
         ports:
           - "80:3000"
         volume:
           - "./:/usr/app"
         environments:
           - env1="balblahlblah"
```

- image ใช้ระบุ Docker image และ tag ที่ต้องการ
