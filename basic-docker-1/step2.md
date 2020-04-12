ทีนี้ เราจะสร้าง image แบบใหม่ ที่ทำงาน แบบตืออเนื่อง และ restart ใหม่เมื่อมีการเปลี่ยนแปลงโค้ด
ให้แก้ไข Dockerfile ตาม บรรทัดข้างล่าง

```
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
