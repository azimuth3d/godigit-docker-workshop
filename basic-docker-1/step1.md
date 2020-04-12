เราจะเริ่มจากสร้าง Docker Image แบบง่ายๆ

ก่อนอื่นสร้างชื่อ Dockerfile ภายใน Folder ที่เราใช้ทำงาน
คลิกขวาที่ /home/godigit/ เลือก new > file ตั้งชื่อเป็น Dockerfile

เสร็จแล้วเราจะสร้าง โค้ดส่วนของ Dockerfile เพื่อใช้ในการสร้าง Image

```
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
