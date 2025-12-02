# Dockerized Python + MySQL Microservice

This project demonstrates a simple microservice architecture using **Docker** and **Docker Compose**.  
A Python application connects to a MySQL database running in a separate container.

---

## 🚀 Features
- Fully containerized Python API
- Separate MySQL database container
- Docker Compose for multi-container orchestration
- Internal networking between services
- Persistent MySQL storage via volumes
- Environment variables for secure configuration

---

## 🗂 Project Structure
```
.
├── app.py
├── requirements.txt
├── Dockerfile
└── docker-compose.yml
```

---

## 🐳 Dockerfile Explanation
```dockerfile
FROM python:3.9
WORKDIR /app
COPY app.py /app/app.py
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

---

## 🐳 docker-compose.yml (Multi-Container Setup)

```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:5000"
    depends_on:
      - db
    environment:
      - DB_HOST=db
      - DB_USER=root
      - DB_PASSWORD=password
      - DB_NAME=testdb

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: testdb
    ports:
      - "3307:3306"
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

---

## ▶️ How to Run

1. Clone the repo  
2. Run:
```
docker-compose up --build
```
3. App runs on **http://localhost:8080**

---

## 📚 Learnings
- Dockerfile creation  
- Python app containerization  
- Multi-container orchestration  
- Networking between containers  
- Persistent storage volumes  
- Environment variable-based configuration  

---

## 🧪 Stopping the Containers
```
docker-compose down
```

---

## 📩 Author
Pallavi Agarwal  
