# SIT323/737 Practical 7P – MongoDB in Kubernetes

This project demonstrates deploying MongoDB in a Kubernetes environment with full CRUD operations, Kubernetes Secrets, service exposure, scheduled backups, and monitoring.

---

## 🧰 Technologies Used

- MongoDB
- Kubernetes (via Docker Desktop)
- MongoDB Compass
- Kubernetes Dashboard
- `kubectl`

---

## 📂 Files Included

| File                         | Description                                 |
|------------------------------|---------------------------------------------|
| `mongo-deployment.yaml`      | MongoDB deployment config with PVC          |
| `mongo-service.yaml`         | NodePort service to expose MongoDB          |
| `mongo-secret.yaml`          | Kubernetes secret for MongoDB credentials   |
| `mongo-backup-cronjob.yaml`  | CronJob for scheduled backups using `mongodump` |
| `mongo-persistent.yaml`      | Combined YAML with StorageClass, PV, PVC    |
| `screenshots/`               | CRUD results, job runs, logs, pod status    |

---

## 🚀 Deployment Instructions

### 1. Clone the Repository

git clone https://github.com/<your-username>/sit323-737-2024-t1-prac7p.git
cd sit323-737-2024-t1-prac7p

2. Apply MongoDB Persistent Setup

kubectl apply -f mongo-persistent.yaml
Ensure this hostPath exists:


C:\sit323_737-2023-t1-prac2p\Week6\MyMappedFolder
3. Expose Service

kubectl apply -f mongo-service.yaml
🔐 MongoDB Credentials
Key	Value
User	admin
Password	password

You can store these as a Kubernetes Secret (mongo-secret.yaml).

🧪 CRUD Testing via MongoDB Compass
Connection URI:


mongodb://admin:password@localhost:32000
Test Steps:
Create DB: testdb

Create Collection: students

Insert, Update, Delete documents

View the collection and document changes

📸 Screenshots saved in screenshots/ folder.

🔁 Backup Setup
To enable backups:


kubectl apply -f mongo-backup-cronjob.yaml
This will:

Run mongodump every 10 mins

Store backups in a temp volume (emptyDir)

You can replace with hostPath for persistence
To check:

kubectl get cronjobs
kubectl get jobs
kubectl get pods
kubectl logs <backup-job-pod>
📈 Monitoring & Logs
You can check MongoDB pod status and logs via:


kubectl get pods
kubectl logs <mongo-pod-name>
Pod status is also visible in the Kubernetes Dashboard UI.
