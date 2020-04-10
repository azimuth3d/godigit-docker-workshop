เราจะเริ่มจากสร้าง Docker Image แบบง่ายๆ

ก่อนอื่นสร้างชื่อ Dockerfile ภายใน Folder ที่เราใช้ทำงาน
คลิกขวาที่ /home/godigit/ เลือก new > file ตั้งชื่อเป็น Dockerfile

เสร็จแล้วเราจะสร้าง โค้ดส่วนของ Dockerfile เพื่อใช้ในการสร้าง Image

```
FROM alpine
CMD ["echo","Hello Docker"]

```
