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
- [Contact](#contact)

---

## Overview

This project implements an AI-powered food recognition system that combines Convolutional Neural Networks (CNN) for image classification and Artificial Neural Networks (ANN) for nutrition estimation. Users can upload food images and receive instant predictions about the food type, nutritional values, and health score.

### Key Capabilities

- Instant food recognition from uploaded images
- Automatic nutrition analysis (calories, protein, carbs, fat)
- Health score calculation based on nutritional content
- RESTful API for easy integration with other applications
- Modular and scalable architecture

---

## Features

### Core Features

- Image-based food classification using CNN
- Nutrition prediction using ANN
- Health score calculation
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
| Environment Management | python-dotenv | 1.0.0 |

---

## System Architecture

The system follows a layered architecture with clear separation of concerns:

Client Application Layer: Web, mobile, or desktop applications that send image upload requests.

API Gateway Layer: FastAPI-based REST endpoints that handle incoming requests and route them to appropriate services.

Preprocessing Layer: Converts uploaded images to the format required by the models (resize, normalize, batch dimension).

CNN Model Layer: Convolutional Neural Network that performs food classification and returns confidence scores.

ANN Model Layer: Artificial Neural Network that predicts nutritional values based on the detected food class.

Health Score Layer: Calculates health scores using nutritional information.

Response Layer: Formats and returns JSON responses with all prediction data.

---

## Project Structure

food-recognition-system/
│
├── config/
│ └── settings.py # Configuration and paths
│
├── utils/
│ ├── labels.py # Food classes and nutrition database
│ └── helper.py # Utility functions
│
├── training/
│ ├── data_loader.py # Training data generation
│ ├── train_ann.py # ANN model training script
│ └── train_cnn.py # CNN model training script
│
├── services/
│ ├── preprocessing.py # Image preprocessing pipeline
│ ├── nutrition_service.py # Nutrition prediction service
│ └── prediction_service.py # Main prediction service
│
├── routes/
│ └── predict.py # API route definitions
│
├── models/
│ ├── cnn_model.keras # Trained CNN model
│ └── ann_model.keras # Trained ANN model
│
├── static/
│ └── uploads/ # Uploaded images storage
│
├── main.py # FastAPI application entry point
├── requirements.txt # Python package dependencies
├── README.md # Project documentation
├── .gitignore # Git ignore file
└── .env.example # Environment variables template



---

## Installation

### Prerequisites

- Python 3.9 or higher
- pip package manager
- Virtual environment (recommended)

### Setup Instructions

**1. Clone the repository**

```bash
git clone https://github.com/yourusername/food-recognition-system.git
cd food-recognition-system

# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python -m venv venv
source venv/bin/activate

pip install -r requirements.txt