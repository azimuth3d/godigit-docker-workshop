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
         volumes:
           - "./:/usr/app"
         environment:
           - env1="balblahlblah"
```

- image ใช้ระบุ Docker image และ tag ที่ต้องการ
- build กำหนด folder ที่อยู่ของไฟล์ Dockerfile เพื่อ ใช้ build image
- ports กำหนด port mapping เพื่อใช้ติดต่อกับภายนอก Container
- volumes กำหนด volume mapping เข้าไปใช้ภายใน container จะเป็น local folder หรือ Docker volume ที่สร้างแยกไว้ก็ได้
- environments ใช้ส่งตัวแปร สิ่งแวดล้อมกับ Container

โครงสร้าง Service ของเราที่จะทำกันใน Workshop นี่คือ !

Nodejs ที่ frontend + backend + db

```yaml
version: "3"
services:
  ghost:
    image: ghost:latest
    restart: always
    depends_on:
      - db
    environment:
      database__client: mysql
      database__connection__host: db
      database__connection__user: root
      database__connection__password: passme
      database__connection__database: ghost
    volumes:
      - ./ghost_content:/var/lib/ghost/content

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: your_database_root_password
    volumes:
      - ./mysql:/var/lib/mysql
```

เริ่มจาก กำหนด services ทั้ง 3 ตัว ใส่ค่า Environment เบื่องต้น บวกกับ port ที่เราติดต่อกับ Container

`docker-compose up -d`
