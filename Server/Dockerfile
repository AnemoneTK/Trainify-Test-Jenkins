# ใช้ Node เวอร์ชัน 18
FROM node:18

WORKDIR /app

# คัดลอก package.json และ package-lock.json (หรือ yarn.lock) มาติดตั้ง dependencies
COPY package*.json ./

# ติดตั้ง dependencies ทั้งหมด
RUN yarn install

# ติดตั้งเพิ่มเติม
RUN yarn add bcryptjs
RUN yarn add ts-node @types/node --dev
RUN yarn add nodemon ts-node --dev

# คัดลอกโค้ดทั้งหมดไปยังคอนเทนเนอร์
COPY . .

# เปิดพอร์ตที่เซิร์ฟเวอร์จะใช้
ENV PORT=3000
EXPOSE 3000

# รันในโหมดพัฒนาโดยใช้ nodemon ชี้ไปที่ไฟล์ server.ts ใน src
CMD ["yarn", "dev"]
