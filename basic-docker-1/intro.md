เราจะมาเริ่มสร้าง Docker image แล้วทำความเข้าใจก็คำสั่งพื้นฐานของ docker กันก่อน

เราจะเริ่มจากสร้าง Docker Image แบบง่ายๆ

ก่อนอื่นสร้างชื่อ Dockerfile ภายใน Folder ที่เราใช้ทำงาน
คลิกขวาที่ /home/godigit/ เลือก new > file ตั้งชื่อเป็น Dockerfile

เสร็จแล้วเราจะสร้าง โค้ดส่วนของ Dockerfile เพื่อใช้ในการสร้าง Image

```Dockerfile
FROM alpine
CMD ["echo","Hello Docker!"]

```

หลังจากนั้น เราก็ไปที่ Terminal ที่อยุ่ด้านล่าง สั่ง

`cd /home/godigit`

เสร็จแล้ว เราจะเสร็จ docker image ที่ชื่อ godigit/hello-docker โดย

`docker build . -t godigit/hello-docker`

แล้ว ลองรัน docker container แรกของเราเลย !

`docker run --rm --name hello godigit/hello-docker`

จะได้ผลตามคำสัั่งที่เราเขียนไว้ใน image คือ echo คำว่า Hello docker! ออกมา

ทีนี้ เราจะสร้าง image แบบใหม่ ที่ทำงาน แบบตืออเนื่อง และ restart ใหม่เมื่อมีการเปลี่ยนแปลงโค้ด
ให้แก้ไข Dockerfile ตาม บรรทัดข้างล่าง

```Dockerfile
FROM node:12-alpine
WORKDIR /usr/app
COPY . .
RUN npm install nodemon -g
CMD ["nodemon","index.js"]
```

`docker build . -t gogidit/node-basic`

เสร็จแล้วเราจะสั่งรัน container ปกติ

`docker --rm --name node-basic godigit/node-basic`
ต่อจากนั้น เราจะเข้า แก้ไขโค้ดที่อยู่ใน container กัน

ก่อนอื่น ให้เปิด terminal ขึ้นอีก 1 tab กดที่ + เลือก Open new terminal
เราจะหา id ของ docker container ที่เราสั่งให้ทำงาน โดย

```
 dockerID=docker ps -a | grep node-basic | awk '{print $1}'
 docker exec -it $dockerID /bin/sh
```

แล้วเข้าไปแก้ไข โดยใช้ vi
`/usr/app# vi index.js`

```
console.log("Listen for editing")
console.log("have edited")
```

เสร็จแล้วมาดูผลที่ Terminal แรกที่เราเปิดทิ้งไว้

จาก part ที่แล้วเราได้เข้าไปแก้ไข ไฟล์ใน Container เพื่อเปลี่ยนแปลงข้อมูล
ทีนี้ เราจะมาลอง Map volume จาก Directory ที่เราทำงาน เข้ากับ Directory ภายใน container
จากนั้นสั่ง run อีกครั้ง โดยการกำหนด -v

`docker run --rm --name node-volume -v ./:/usr/app godigit/node-basic`

ลองแก้ไขไฟล์ใน Directory ดูก็ จะเห็นผลการเปลี่ยนใน Container ด้วย
