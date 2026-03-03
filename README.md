# 🌾 Crop Yield Prediction System (Machine Learning Based)

A production-ready Machine Learning web application built using **Flask** and **Scikit-Learn** to predict crop yield based on environmental and agricultural factors.

This system uses a trained **Decision Tree Regressor** model along with a preprocessing pipeline to deliver accurate yield predictions via a modern web interface.

---

# 📌 Project Overview

The Crop Yield Prediction System estimates agricultural yield using the following input parameters:

* Year
* Average Rainfall (mm per year)
* Pesticides Used (tonnes)
* Average Temperature (°C)
* Area (Region/Country)
* Crop Item

The system integrates:

* Data preprocessing pipeline
* Trained regression model
* Flask backend
* Aesthetic frontend interface

---

# 🗂️ Project Structure

```
02 Crop Yield/
│
├── Data/
│   └── CropYield_dataset.csv
│
├── EDA and Training/
│   └── Training.ipynb
│
├── models/
│   ├── dtr.pkl
│   └── preprocessor.pkl
│
├── templates/
│   └── index.html
│
├── app.py
├── requirements.txt
└── README.md
```

---

# 🏗️ High Level Design (HLD)

## 1️⃣ System Architecture Overview

```
User → Web UI → Flask Backend → Preprocessor → ML Model → Prediction → UI Response
```

## 2️⃣ Component Interaction Flow

1. User enters crop-related inputs via web form.
2. Frontend sends POST request to `/predict`.
3. Flask backend:

   * Extracts form data
   * Converts input into NumPy array
   * Applies preprocessing pipeline
4. Transformed data is passed to trained Decision Tree Regressor.
5. Model generates prediction.
6. Result is rendered back on the UI.

---

## 3️⃣ Architectural Layers

### 🔹 Presentation Layer

* HTML (templates/index.html)
* CSS (embedded styling)
* Handles user interaction

### 🔹 Application Layer

* Flask (app.py)
* Handles routing and request processing

### 🔹 Machine Learning Layer

* preprocessor.pkl (ColumnTransformer / Pipeline)
* dtr.pkl (DecisionTreeRegressor)

### 🔹 Data Layer

* CropYield dataset
* Used during training phase

---

# 🔍 Low Level Design (LLD)

## 1️⃣ Backend Module: app.py

### Flask Initialization

```python
app = Flask(__name__)
```

### Model Loading

```python
dtr = pickle.load(open('models/dtr.pkl','rb'))
preprocessor = pickle.load(open('models/preprocessor.pkl','rb'))
```

### Route: `/`

* Method: GET
* Returns: index.html

### Route: `/predict`

* Method: POST
* Steps:

  1. Capture form inputs
  2. Create NumPy feature array
  3. Apply preprocessing transformation
  4. Perform model prediction
  5. Return prediction to UI

---

## 2️⃣ Data Preprocessing Design

The preprocessing pipeline typically includes:

* Handling categorical features (Area, Item)

  * OneHotEncoding
* Scaling numerical features (if used)
* ColumnTransformer integration

Output:

```
Raw Input → Transformed Feature Vector → Model Input
```

---

## 3️⃣ Machine Learning Model

### Algorithm Used:

Decision Tree Regressor

### Why Decision Tree?

* Handles non-linear relationships
* Works with mixed data types
* No scaling mandatory
* Interpretable structure

### Model Serialization

* Stored using `pickle`
* Loaded at application startup

---

## 4️⃣ Frontend Design Logic

### Form Inputs

Each input field is mapped exactly to backend variable names:

| Frontend Name                 | Backend Variable              |
| ----------------------------- | ----------------------------- |
| Year                          | Year                          |
| average_rain_fall_mm_per_year | average_rain_fall_mm_per_year |
| pesticides_tonnes             | pesticides_tonnes             |
| avg_temp                      | avg_temp                      |
| Area                          | Area                          |
| Item                          | Item                          |

### Prediction Rendering

```html
{% if prediction %}
  {{ prediction[0][0] }}
{% endif %}
```

---

# ⚙️ Installation & Setup

## 1️⃣ Clone Repository

```bash
git clone <repository-url>
cd 02-Crop-Yield
```

## 2️⃣ Create Virtual Environment

```bash
python -m venv venv
source venv/bin/activate
```

(Windows)

```bash
venv\Scripts\activate
```

## 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

## 4️⃣ Run Application

```bash
python app.py
```

Application runs at:

```
http://127.0.0.1:5000/
```

---

# 📡 API Contract

## Endpoint: `/predict`

**Method:** POST
**Content-Type:** Form Data

### Input Schema

```
Year: int
average_rain_fall_mm_per_year: float
pesticides_tonnes: float
avg_temp: float
Area: string
Item: string
```

### Output

Rendered HTML page with predicted crop yield.

---

# 🧠 Model Training Workflow

1. Data Collection
2. Data Cleaning
3. Feature Engineering
4. Train-Test Split
5. Model Training
6. Evaluation (R², MAE, MSE)
7. Model Serialization (pickle)

---

# 📊 Tech Stack

* Python 3.x
* Flask
* NumPy
* Scikit-learn
* Pandas
* HTML5 / CSS3
* Pickle (Model Serialization)

---

# 🚀 Future Enhancements

* Convert to REST API (JSON-based)
* Deploy on AWS / Azure / GCP
* Add model monitoring
* Add feature importance visualization
* Integrate multiple ML models
* Add authentication system
* Dockerize application
* CI/CD integration

---

# 📈 Scalability Considerations

* Model can be wrapped in REST API (FastAPI)
* Load balancing via Nginx
* Containerization using Docker
* Cloud deployment
* Model versioning

---

# 🔒 Security Improvements (Recommended)

* Input validation
* CSRF protection
* Rate limiting
* Environment variable configuration
* Secure model storage

---

# 👨‍💻 Author

Zainul Abedeen

---

# Connect Me

## [GitHub](https://github.com/zainulabedeen589)

## [LinkedIn](https://www.linkedin.com/in/zainulabedeen589/)

---
