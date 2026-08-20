# AI-Powered Food Recognition & Nutrition Analysis System

A deep learning-based food recognition system that identifies food items from images and predicts their nutritional values using CNN and ANN models.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Training Models](#training-models)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Workflow](#workflow)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This project implements an AI-powered food recognition system that combines Convolutional Neural Networks (CNN) for image classification and Artificial Neural Networks (ANN) for nutrition estimation. Users can upload food images and receive instant predictions about the food type, nutritional values, and health score.

### Key Capabilities

- Instant food recognition from uploaded images
- Automatic nutrition analysis (calories, protein, carbs, fat)
- Health score calculation based on nutritional content
- RESTful API for easy integration
- Modular and scalable architecture

---

## Features

### Core Features

- Image-based food classification using CNN
- Nutrition prediction using ANN
- Health score calculation (1-10)
- REST API with FastAPI
- Automatic image storage with unique identifiers
- Fallback mechanism when models are unavailable
- Support for JPG and PNG image formats

### Technical Features

- Modular architecture for maintainability
- GPU support for faster training
- Configurable settings via environment variables
- Type hints for better code documentation
- Error handling and graceful degradation

---

## Tech Stack

| Component | Technology | Version |
|-----------|------------|---------|
| Web Framework | FastAPI | 0.104.1 |
| Deep Learning | TensorFlow | 2.13.0 |
| Image Processing | Pillow | 10.1.0 |
| Numerical Computing | NumPy | 1.24.3 |
| Server | Uvicorn | 0.23.2 |
| Language | Python | 3.9+ |

---

## System Architecture

The system follows a layered architecture with clear separation of concerns:

**Client Application Layer**: Web, mobile, or desktop applications that send image upload requests.

**API Gateway Layer**: FastAPI-based REST endpoints that handle incoming requests and route them to appropriate services.

**Preprocessing Layer**: Converts uploaded images to the format required by the models (resize, normalize, batch dimension).

**CNN Model Layer**: Convolutional Neural Network that performs food classification and returns confidence scores.

**ANN Model Layer**: Artificial Neural Network that predicts nutritional values based on the detected food class.

**Health Score Layer**: Calculates health scores using nutritional information.

**Response Layer**: Formats and returns JSON responses with all prediction data.

---

## Project Structure
food-recognition-system/
│
├── config/
│ └── settings.py # Configuration settings
│
├── utils/
│ ├── labels.py # Food classes and nutrition DB
│ └── helper.py # Utility functions
│
├── training/
│ ├── data_loader.py # Generate training data
│ ├── train_ann.py # Train ANN model
│ └── train_cnn.py # Train CNN model
│
├── services/
│ ├── preprocessing.py # Image preprocessing
│ ├── nutrition_service.py # Nutrition prediction
│ └── prediction_service.py # Main prediction service
│
├── routes/
│ └── predict.py # API endpoints
│
├── models/
│ ├── cnn_model.keras # Trained CNN model
│ └── ann_model.keras # Trained ANN model
│
├── static/
│ └── uploads/ # Uploaded images
│
├── main.py # FastAPI application
├── requirements.txt # Python dependencies
├── README.md # This file
├── .gitignore # Git ignore file
└── .env.example # Environment variables template

---

## Installation

### Prerequisites

- Python 3.9 or higher
- pip package manager
- Virtual environment (recommended)

### Step-by-Step Setup

```bash
# 1. Clone the repository
git clone https://github.com/avvyas1000-gif/food-recognition-system.git
cd food-recognition-system

# 2. Create virtual environment
python -m venv venv

# 3. Activate virtual environment
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

# 4. Install dependencies
pip install -r requirements.txt

# 5. Create required directories
mkdir -p models static/uploads

# 6. Train models
python -m training.train_ann
python -m training.train_cnn

# 7. Start the server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload

Training Models
Train ANN Model-
python -m training.train_ann

Train CNN Model-
python -m training.train_cnn

Model Architectures
CNN Architecture:

Input: 128x128x3 RGB images

Convolutional layers with MaxPooling

Dense layers for classification

Output: Food class probabilities

ANN Architecture:

Input: Food class encoding + portion scale

Hidden layers with ReLU activation

Output: Calories, protein, carbs, fat


Make Predictions
Using Python:

python
import requests

url = "http://localhost:8000/api/predict"
files = {"file": open("pizza.jpg", "rb")}
response = requests.post(url, files=files)
print(response.json())
Using cURL:

bash
curl -X POST "http://localhost:8000/api/predict" -F "file=@pizza.jpg"
Sample Response
json
{
    "food": "Pizza",
    "confidence": 96.5,
    "nutrition": {
        "calories": 266.0,
        "protein": 11.0,
        "carbs": 33.0,
        "fat": 10.0
    },
    "health_score": 8.2,
    "image_url": "/static/uploads/93ac67fd.jpg"
}
API Documentation
POST /api/predict
Request:

Parameter	Type	Description	Required
file	File	Image file (JPG, PNG, JPEG)	Yes
Success Response (200):

json
{
    "food": "Pizza",
    "confidence": 96.5,
    "nutrition": {
        "calories": 266.0,
        "protein": 11.0,
        "carbs": 33.0,
        "fat": 10.0
    },
    "health_score": 8.2,
    "image_url": "/static/uploads/93ac67fd.jpg"
}
Error Response (400):

json
{
    "detail": "Uploaded file is not an image."
}
GET /health
Health check endpoint.

json
{
    "status": "healthy"
}
Workflow
The complete system workflow processes images through multiple stages:

Image Upload

User submits an image in JPG or PNG format

HTTP server receives the request

Preprocessing

Bytes converted to file object using io.BytesIO

PIL Image reads the image as an object

Image resized to 128x128 pixels

Image converted to array format

Pixel values normalized to 0-1

Batch dimension added for model input

Food Classification

CNN model predicts the food class

Confidence score is calculated

Nutrition Estimation

ANN model predicts nutritional values

If model unavailable, nutrition database is used as fallback

Health Score Calculation

Health score calculated based on nutrition data

Image Storage

Unique filename generated using UUID

Image saved to static/uploads directory

Response Generation

JSON response with all prediction data

Image URL included in the response

Contributing
Contributions are welcome. Follow these steps:

Fork the repository

Create a feature branch

Make your changes

Commit your changes

Push to your fork

Open a pull request

License
This project is licensed under the MIT License.

Contact
GitHub: avvyas1000-gif

Email: avvyas1000@gmail.com

Acknowledgments
FastAPI for the web framework

TensorFlow for deep learning

Food-101 dataset for training

USDA Food Database for nutrition information

Roadmap
Support for 200+ food classes

Real-time video recognition

Mobile application development

Cloud deployment

User authentication

Requirements
text
fastapi==0.104.1
uvicorn==0.23.2
tensorflow==2.13.0
pillow==10.1.0
numpy==1.24.3
python-multipart==0.0.6
pydantic==2.4.2
python-dotenv==1.0.0
scikit-learn==1.3.0
matplotlib==3.7.2
Built with FastAPI and TensorFlow.

text

---
#Acknowledgments
"Special thanks to my mentor Saurabh Soni(Generative AI Engineer,REGex Software Services) for valuable guidance and support throughout the project."

