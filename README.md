# Insurance Premium Prediction API 🏥💰
- A FastAPI-based machine learning microservice that predicts insurance premium categories using demographic, geographic, and health data with confidence scoring and comprehensive validation.This project is a production-grade Insurance Premium Prediction API built using the FastAPI framework. Its primary function is to act as a machine learning microservice that automatically categorizes users into insurance premium risk brackets (such as Low, Medium, or High) based on their personal information. It ingests a user's demographic, geographic, and health data, processes it through a pre-trained machine learning model, and returns a prediction accompanied by a confidence score and a detailed breakdown of the factors influencing the decision. This provides transparency and valuable insight for underwriters, agents, or customers using the system.
---
#### 🚀 Key Features

##### Core Functionality
- **Premium Category Prediction**: Classifies users into Low/Medium/High premium categories
- **Confidence Scoring**: Provides probability-based confidence levels (0.0-1.0)
- **Risk Factor Analysis**: Identifies key contributors to premium decisions
- **Real-time Predictions**: Instant API responses with structured data

##### Technical Excellence
- ✅ **Production-Ready Architecture**: Modular design with separation of concerns
- ✅ **Comprehensive Validation**: Pydantic models with custom field validators
- ✅ **Health Monitoring**: System metrics and model status endpoints
- ✅ **Error Handling**: Robust try-catch blocks with graceful degradation
- ✅ **Version Management**: Model version tracking and traceability

##### 🛠️ Technical Stack
- **Backend Framework**: FastAPI with Python 3.8+
- **Machine Learning**: Scikit-learn with pre-trained model
- **Validation**: Pydantic with custom validators
- **Data Processing**: Pandas, NumPy
- **API Documentation**: Automatic Swagger/OpenAPI
- **Deployment**: Uvicorn ASGI server
---
#### 📁 Project Structure
```
insurance-api/
├──> app.py                 # Main FastAPI application
├──> requirements.txt       # Python dependencies
├──> schemas/
│   ├──> user_input.py     # Pydantic models for input validation
│   └──> prediction_response.py  # Response models
├──> models/
│   └──> predict.py        # ML model loading and prediction logic
├──> utils/
│   └──> city_tier.py      # City classification system
└──> model/
    └──> prajwalmodel.pkl  # Pre-trained ML model
```
---
#### 🔌 API Endpoints

##### 1. Home Endpoint (/)
```
 GET /
```
- Welcome message and API information
- Usage guidelines and endpoint overview
- Purpose: Root endpoint for basic API discovery

##### 2. Health Check Endpoint (/health)
```
GET /health
```
- **Machine-readable status**: System health monitoring
- **Model status**: Loading state and version information
- **System metrics**: CPU, memory, disk usage
- **Dependency versions**: Package compatibility info
- **Purpose**: Load balancer health checks and monitoring
--
##### 3. Prediction Endpoint (/predict)
```
POST /predict
```
- **Input**: User demographic and health data
- **Output**: Predicted premium category with confidence scores
- **Features**: Risk factors, probability distribution, premium estimates
- **Purpose**: Main prediction functionality
---
#### 📊 Input Data Model
```
{
  "age": 35,
  "weight": 72.5,
  "height": 1.78,
  "income_lpa": 12.5,
  "smoker": false,
  "city": "Mumbai",
  "occupation": "private_job"
}
```
##### Validation Features:
- **Age**: 1-119 years with business logic checks
- **City**: Automatic normalization and tier classification
- **Occupation**: Strict enum validation with predefined categories
- **BMI**: Calculated automatically from weight/height
- **Income**: LPA (Lakhs Per Annum) validation
---
#### 🎯 Output Response
```
{
  "predicted_category": "Medium",
  "confidence": 0.8432,
  "class_probabilities": {
    "Low": 0.01,
    "Medium": 0.15,
    "High": 0.84
  },
  "model_version": "1.0.0",
  "prediction_timestamp": "2024-01-15T10:30:00Z",
  "risk_factors": ["smoker", "high_bmi"],
  "recommended_premium_range": {
    "min": 15000,
    "max": 30000,
    "recommended": 22500
  }
}
``` 
---
#### 🌟 Advanced Features
--
##### City Tier System
- **Tier 1 Cities**: Mumbai, Delhi, Bangalore, etc. (8 cities)
- **Tier 2 Cities**: Jaipur, Chandigarh, Pune, etc. (50+ cities)
- **Tier 3**: All other cities
- Automatic classification with case normalization

##### Risk Assessment Engine
- **Lifestyle Risk**: Smoking + BMI combination scoring
- **Age Groups**: Young/Adult/Middle-aged/Senior categorization
- **Geographic Risk**: City tier-based risk adjustment
- **Comprehensive Scoring**: Multi-factor risk assessment

##### Production Features
- **Model Versioning**: Track and manage model deployments
- **Error Handling**: Comprehensive exception management
- **Logging**: Detailed application logging for debugging
- **API Documentation**: Automatic OpenAPI/Swagger generation
- **Health Monitoring**: Real-time system status reporting
---
#### 🚀 Deployment Ready
##### Cloud Native Features
- **Health Checks**: Ready for Kubernetes liveness/readiness probes
- **Load Balancer Compatible**: Proper health endpoint for AWS/cloud platforms
- **Metrics Exposure**: System resource monitoring endpoints
- **Scalable Design**: Stateless architecture for horizontal scaling
---
##### Development Setup
###### Install dependencies
```
pip install -r requirements.txt
```
###### Run development server
```
uvicorn app:app --reload 
```
```
# Access documentation
# http://localhost:8000/docs
```
---
##### API Endpoints and Production Readiness
###### The API exposes several well-defined endpoints crucial for both functionality and operational health:
- The Root endpoint **(/)** provides a human-readable welcome message and guides users to other available endpoints.
- The Health Check endpoint **(/health)** is machine-readable and is vital for production deployment. It returns the status of the application, the loaded model's version, and key system metrics (CPU, Memory, Disk usage). This allows cloud platforms like AWS or Kubernetes load balancers to verify the application's health and route traffic accordingly.
- The Prediction endpoint **(/predict)** is the core of the service, accepting validated user data and returning the prediction result.
---
##### Robustness and Validation Features
- A key focus of the project is robustness. Comprehensive try-catch blocks and HTTP exception handling ensure the API gracefully manages errors—such as an invalid input or a model that fails to load—without crashing. It provides clear, structured error messages back to the client. The validation system is extensive, checking for correct data types, value ranges (e.g., age must be between 1-119), and business logic (e.g., a user under 18 must have an occupation of 'student').

---
##### Advanced Output and Explainability
- Beyond a simple prediction, the API's response is designed for explainability and actionability. It doesn't just return a category; it provides a confidence score (a value between 0.0 and 1.0 derived from the model's probability output) and the full probability distribution across all possible categories. Furthermore, it includes a list of identified risk factors (e.g., ["smoker", "obese_bmi"]) and even a recommended premium range in rupees, giving clear reasons behind the prediction and its potential financial implication.
---
##### Development and Deployment Setup
- The project includes a requirements.txt file generated via pip freeze, which pins all necessary dependencies (FastAPI, Uvicorn, Pydantic, Scikit-learn, Pandas, etc.) to ensure a consistent and reproducible environment across development and production. The application is run using Uvicorn, a high-performance ASGI server, with hot-reload capabilities enabled for development. 
---
#### 📈 Use Cases
- **Insurance Companies**: Automated underwriting support
- **Field Agents**: Mobile premium estimation tool
- **Customer Portals**: Online premium calculators
- **Underwriting Teams**: Risk assessment augmentation
- **API Consumers**: Integration with existing systems
---
#### 🔮 Future Enhancements
- **MLflow Integration**: Model registry and experiment tracking
- **Authentication**: JWT/OAuth2 security
- **Rate Limiting**: API usage controls
- **Database Integration**: Prediction history storage
- **Advanced Monitoring**: Prometheus metrics, Grafana dashboards
- **A/B Testing**: Multiple model version support

---
##### Conclusion and Value Proposition
***In summary, this project successfully transforms a simple machine learning script into a professional, self-documenting, and resilient web service. It encapsulates best practices for API design, including validation, error handling, logging, and system monitoring. The API is not only ready for integration into front-end applications but is also prepared for deployment in a cloud-native environment, providing a reliable and insightful tool for automating and supporting insurance premium assessment.***

---

## Before Improvement
- This demo showcases the initial, minimal viable product (MVP). It was a simple Python script with a single function. The user had to manually prepare their data in the exact format the model expected, with no validation. The script would often crash with cryptic errors for invalid inputs. The output was just a plain text category (e.g., "High") with no context, no confidence score, and no explanation. It was a proof-of-concept that worked but was completely unsuitable for integration into any application or use by anyone other than the developer.
----
##### Key Characteristics of the "Before" State:
- **No API**: Just a Python function in a script.
- **No Validation**: Input errors caused crashes.
- **No Explanation**: Output was just a category label.
- **No Structure**: No standard way to send or receive data.
- **Fragile**: Any unexpected input would break it.
----
###### Video Title: Insurance Predictor - Basic minimal viable product  Demo
###### Video: 
https://github.com/user-attachments/assets/c61ab74f-cecb-4bf1-aec0-59544962600c


---
## After Improvement (Production API)
- This walkthrough demonstrates the fully featured, production-grade API. We start at the automatically generated Interactive Documentation (/docs), a hallmark of FastAPI, which allows users to test the API directly from their browser.

   - 1) **Testing the Health Endpoint (/health)**: We first call the health check to see the system status, confirming the model is loaded and showing system metrics. This is crucial for DevOps and cloud deployment.

   - 2) **Making a Prediction (/predict)**: We use the docs interface to send a structured JSON request. The video highlights:

      - **Automatic Validation**: Trying to send an invalid city name or a negative age results in a clear, helpful error message instantly, without even touching the ML model.
      - **Rich, Structured Response**: The response is not just a category. It includes the confidence score (e.g., 0.92), the probability breakdown for all categories, the model version used, and a list of identified risk factors (e.g., ["smoker", "senior_age"]).

   - 3) **Demonstrating Robustness**: We show how the API gracefully handles edge cases, like a city not in the predefined list (it defaults to "Tier 3"), thanks to the comprehensive error handling and data validation layers.

---
##### Key Characteristics of the "After" State:

- **Professional API**: Built with FastAPI, featuring auto-generated interactive documentation.
- **Robust Validation**: Comprehensive input checking with clear error messages.
- **Explainable AI**: Responses include confidence scores and risk factors.
- **Production Ready**: Includes health checks, system monitoring, and version tracking.
- **Developer & User Friendly**: Easy to understand, integrate, and use.

###### Video Title: Insurance Predictor API - Production Ready Walkthrough
###### Video:
https://github.com/user-attachments/assets/73832f15-7df3-4d1c-800e-ab6f60ea563d
https://github.com/user-attachments/assets/13e3d714-732e-435a-a70a-5b3e37269357

