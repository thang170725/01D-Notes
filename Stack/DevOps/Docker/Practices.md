- [Các đóng gói dự án FE - BE - DB kiến trúc Modular Monolith thành 3 Docker](#các-đóng-gói-dự-án-fe---be---db-kiến-trúc-modular-monolith-thành-3-docker)
---
# Các đóng gói dự án FE - BE - DB kiến trúc Modular Monolith thành 3 Docker
```bash
project-root/
├── frontend/
└── backend/
```
**Step 1: Tạo backend/Dockerfile & frontend/Dockerfile** 
```bash
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```
```bash
FROM node:20

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host"]
```
**Step 2: Tạo docker-compose.yml ở root**
```bash
version: "3.9"

services:
  db:
    image: mariadb:11
    container_name: mariadb_container
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: SmartRecipe
      MYSQL_USER: ai_user
      MYSQL_PASSWORD: ai123
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql

  backend:
    build: ./backend
    container_name: backend_container
    restart: always
    env_file:
      - ./backend/.env
    ports:
      - "3651:3651"
    depends_on:
      - db

  frontend:
    build: ./frontend
    container_name: frontend_container
    restart: always
    ports:
      - "5173:5173"
    depends_on:
      - backend

volumes:
  db_data:
```
**Step 3: Chạy dự án ở thư mục root**
```bash
docker compose up --build
```
