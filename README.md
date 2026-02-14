

🚀 DWOMS

Digital Workflow & Operations Management System

A full-stack role-based factory management system built using:

⚛ React (TypeScript)

🔥 Firebase Authentication

📦 Cloud Firestore

🎨 TailwindCSS + ShadCN UI

📊 Real-time Dashboard

📁 CSV & PDF Reports Export



---

📌 Project Overview

DWOMS is a web-based system designed for small and medium manufacturing units to manage:

👷 Workers

🏭 Production

📦 Inventory

📝 Tasks

📊 Reports

🔐 Role-Based Access Control


This project was developed as a college learning project to understand:

Backend integration

Firebase authentication

Firestore database

Role-based routing

Real-time data handling



---

🏗 System Architecture

Frontend → React + TypeScript
Backend → Firebase (Auth + Firestore)
Database → Cloud Firestore
Authentication → Firebase Email/Password


---

👥 User Roles

Role	Access

🛡 Admin	Full system access
👨‍💼 Supervisor	Production + Tasks + Reports
👷 Worker	Production + Assigned Tasks
👀 Client	Read-only dashboard



---

🔐 Authentication Flow

Users are created in Firebase Authentication

Corresponding user document is stored in:

users/{uid}

Role is stored in Firestore

Protected routes validate:

Auth status

Role-based permissions




---

📂 Firestore Database Structure

1️⃣ users Collection

users/{uid}
{
  name: string
  email: string
  role: "admin" | "supervisor" | "worker" | "client"
  createdAt: timestamp
}


---

2️⃣ tasks Collection

tasks/{taskId}
{
  productType: string
  assignedWorkerId: string
  assignedWorkerName: string
  status: "Assigned" | "In Progress" | "Quality Check" | "Completed"
  estimatedTime: number
  createdBy: string (admin uid)
  timestamp: timestamp
  completedAt?: timestamp
}


---

3️⃣ inventory Collection

inventory/{itemId}
{
  itemName: string
  currentStock: number
  minStockLevel: number
  unit: string
  lastUpdated: timestamp
}


---

4️⃣ production Collection

production/{entryId}
{
  workerId: string
  workerName: string
  productName: string
  quantity: number
  shift: "morning" | "afternoon" | "night"
  date: string
  timestamp: timestamp
}


---

📊 Features

✅ Dashboard

Today's Production

Active Tasks

Completed Tasks

Low Stock Alerts

Worker Productivity Ranking



---

✅ Task Management

Create task (Admin/Supervisor)

Role-based task visibility

Task workflow:

Assigned → In Progress → Quality Check → Completed



---

✅ Inventory Management

Add items

Stock In / Stock Out

Low stock detection

Real-time updates



---

✅ Production Entry

Worker production logging

Real-time Firestore storage

Dashboard auto update



---

✅ Reports

Filter by date range

Export to:

📄 PDF

📊 CSV


Production Report

Tasks Report

Inventory Report



---

🛡 Firestore Security Rules (Sample)

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    function isAuthenticated() {
      return request.auth != null;
    }

    match /users/{userId} {
      allow read, write: if isAuthenticated();
    }

    match /inventory/{docId} {
      allow read, write: if isAuthenticated();
    }

    match /production/{docId} {
      allow read, write: if isAuthenticated();
    }

    match /tasks/{docId} {
      allow read, write: if isAuthenticated();
    }
  }
}


---

⚙️ Installation Guide

1️⃣ Clone Repository

git clone https://github.com/your-username/dwoms.git
cd dwoms


---

2️⃣ Install Dependencies

npm install


---

3️⃣ Configure Firebase

Create:

src/firebase/config.ts

Add your Firebase config:

import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
import { getFirestore } from "firebase/firestore";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
};

const app = initializeApp(firebaseConfig);

export const auth = getAuth(app);
export const db = getFirestore(app);


---

4️⃣ Run Project

npm run dev


---

🎓 Learning Outcomes

This project helped in understanding:

Firebase Authentication integration

Firestore CRUD operations

Real-time listeners (onSnapshot)

Role-based route protection

Production workflow design

Inventory logic

State management

Error debugging

Full project deployment flow



---

🧠 Future Improvements

🔄 Automatic user creation on signup

📈 Charts using Recharts

📦 Batch production stock automation

🔐 Stronger security rules

🧾 Audit logs

📱 Mobile responsive optimization

🌍 Deployment to Firebase Hosting



---

👨‍💻 Developed By

Teja Bharadwaj(Backend) and Shreyas(Frontend)

---

📜 License

This project is built for educational purposes.


---

