# FastAPI Book Project

🚀 **A FastAPI-based book management API with CI/CD integration and Nginx reverse proxy.**

---

## **🛠️ Features**
✅ Retrieve books by ID  
✅ CI/CD Pipeline with GitHub Actions  
✅ Automatic deployment to EC2  
✅ Nginx reverse proxy setup  

---

## **🚀 Getting Started**

### **1️⃣ Clone the Repository**
```bash
git clone https://github.com/your-username/fastapi-book-project.git
cd fastapi-book-project
```

### **2️⃣ Create a Virtual Environment**
```bash
python -m venv venv
source venv/Scripts/activate  # On Windows use: venv\Scripts\activate
```

### **3️⃣ Install Dependencies**
```bash
pip install -r requirements.txt
```

### **4️⃣ Run the Application Locally**
```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
Your API will be available at:  
👉 **http://127.0.0.1:8000/docs**  

---

## **🛠️ API Endpoints**

### 📚 **Retrieve a Book by ID**
- **Endpoint:** `GET /api/v1/books/{book_id}`  
- **Response:**  
  - `200 OK` → Returns book details  
  - `404 Not Found` → If book does not exist  
- **Example Response:**
  ```json
  {
      "id": 1,
      "title": "The Pragmatic Programmer",
      "author": "Andrew Hunt & David Thomas",
      "year": 1999
  }
  ```

---

## **✅ CI/CD Setup**

This project includes a **CI/CD pipeline** using **GitHub Actions**:
- **Continuous Integration (CI):** Runs tests on every pull request to `main`.  
- **Continuous Deployment (CD):** Deploys automatically on merging to `main`.  

📌 **GitHub Actions Workflow Files:**  
- `.github/workflows/ci.yml` – Runs tests on pull requests  
- `.github/workflows/cd.yml` – Deploys the app on EC2  

---

## **🖥️ Deployment Instructions**

### **1️⃣ Set Up an EC2 Server**
- Launch an **Ubuntu EC2 instance**  
- Open **port 22 (SSH), 80 (HTTP), and 443 (HTTPS)** in **Security Groups**  

### **2️⃣ Configure Nginx as a Reverse Proxy**
Edit your Nginx config (`/etc/nginx/sites-available/fastapi`):  
```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```
Enable the config:
```bash
sudo ln -s /etc/nginx/sites-available/fastapi /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

### **3️⃣ Deploy Using GitHub Actions**
- Add your **EC2 SSH key** to GitHub Secrets:  
  - `SSH_PRIVATE_KEY`, `SERVER_USER`, `SERVER_IP`  
- Push to `main`, and GitHub Actions will deploy automatically.

---

## **🔗 Live API**
🌍 **Base URL:** `http://13.61.11.120`  
📄 **Swagger Docs:** `http://13.61.11.120/docs`  
   **Book endpoint** `http://13.61.11.120/api/v1/books/2`

---

## **👨‍💻 Contributors**
- **Azeezat Omobolanle Nasir**  

---