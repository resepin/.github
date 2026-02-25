# 🍳 Resep.in Organization

[![Azure](https://img.shields.io/badge/Deploy-Azure_App_Service-0078D4?style=flat-square&logo=microsoft-azure&logoColor=white)]()
[![Laravel](https://img.shields.io/badge/Web-Laravel_11-FF2D20?style=flat-square&logo=laravel&logoColor=white)]()
[![FastAPI](https://img.shields.io/badge/API-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)]()
[![YOLOv8](https://img.shields.io/badge/AI-YOLOv8-FF9D00?style=flat-square&logo=ultralytics&logoColor=white)]()
[![MLOps](https://img.shields.io/badge/MLOps-DVC_%7C_MLflow-4181FF?style=flat-square)]()

**Empowering home cooks through Computer Vision and AI.**

Welcome to the official GitHub organization for **Resep.in**. We are building an intelligent, AI-powered recipe discovery ecosystem that bridges the gap between the ingredients in your fridge and the meals on your table. By integrating state-of-the-art object detection with a robust backend architecture, Resep.in automatically identifies food ingredients from images and curates highly relevant culinary recommendations.

---

## 🏗️ System Architecture

The Resep.in platform is built on a microservices-inspired architecture, separating the user-facing web application, the AI inference engine, and the machine learning pipeline to ensure high availability, scalability, and maintainability.

### 🌐 Core Repositories

| Repository | Role | Tech Stack | Status |
| :--- | :--- | :--- | :--- |
| 🍴 **[resepin](https://github.com/resepin/resepin)** | **Frontend & API Gateway**<br>The primary web application handling user authentication, UI/UX, and orchestration. It communicates with the Spoonacular API for recipe fetching and our internal AI API for image processing. | Laravel, PHP, MySQL | 🟢 Production (Azure) |
| 🧠 **[ingredient-ai](https://github.com/resepin/ingredient-ai)** | **AI Inference Microservice**<br>A high-performance, containerized REST API serving our custom YOLOv8 model. Optimized for sub-100ms CPU inference using ONNX, multi-threading (Gunicorn/Uvicorn), and integrated with Azure Application Insights for P50/P99 latency tracking. | FastAPI, Python, ONNX | 🟢 Production (Azure) |
| 📊 **[resepin-ml-train](https://github.com/resepin/resepin-ml-train)** | **MLOps & Training Pipeline**<br>The research and model training workspace. Contains the Jupyter Notebooks used to train the object detection model using an Nvidia RTX 5070 GPU. Implements strict MLOps standards for dataset and experiment tracking. | PyTorch, DVC, MLflow | 🟡 Active Development |

---

## ⚙️ MLOps & Data Pipeline

Our machine learning lifecycle strictly adheres to modern MLOps practices to ensure reproducibility and team collaboration:

* **Data Version Control (DVC):** Heavy binary files, including image datasets and model weights (`.pt`), are tracked using DVC and stored remotely in Google Drive. Git tracks the lightweight `.dvc` pointers.
* **Experiment Tracking (MLflow):** Every training run, hyperparameter adjustment, and resulting metric (mAP, loss) is logged via MLflow, providing a clear lineage from code commit to model artifact.

---

## 🚀 Getting Started

If you are a developer looking to set up the Resep.in environment locally, please follow this standard workflow:

### 1. Model Preparation
Clone the training repository and pull the dataset from our remote storage:
```bash
git clone [https://github.com/resepin/resepin-ml-train.git](https://github.com/resepin/resepin-ml-train.git)
cd resepin-ml-train
dvc pull  # Requires authorized access to the Google Drive remote
```

### 2. Inference API Setup
Initialize the FastAPI server to serve the exported .onnx model locally:
```bash
git clone [https://github.com/resepin/ingredient-ai.git](https://github.com/resepin/ingredient-ai.git)
cd ingredient-ai
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

### 3. Web Application
Run the Laravel application and link it to your local AI inference endpoint and the Spoonacular API:
```bash
git clone [https://github.com/resepin/resepin.git](https://github.com/resepin/resepin.git)
cd resepin
composer install
cp .env.example .env
php artisan key:generate
php artisan serve
```

---

## 🛡️ License & Contributing
Currently, the Resep.in repositories are maintained by the core development team. If you discover any issues or wish to propose architectural improvements, please open an issue in the respective repository.

Resep.in — Cook smarter, not harder.
