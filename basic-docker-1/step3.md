จาก part ที่แล้วเราได้เข้าไปแก้ไข ไฟล์ใน Container เพื่อเปลี่ยนแปลงข้อมูล
ทีนี้ เราจะมาลอง Map volume จาก Directory ที่เราทำงาน เข้ากับ Directory ภายใน container
จากนั้นสั่ง run อีกครั้ง โดยการกำหนด -v

`docker run --rm --name node-volume -v ./:/usr/app godigit/node-basic`

ลองแก้ไขไฟล์ใน Directory ดูก็ จะเห็นผลการเปลี่ยนใน Container ด้วย
