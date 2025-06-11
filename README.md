
---

# 🧮 Assignment Problem Solver – Enterprise-Ready Optimization Tool

##  Overview
This project solves the classic **Assignment Problem** using the **Hungarian Algorithm** (a.k.a. Munkres algorithm), which is designed to minimize the total cost of assigning agents (e.g., employees, machines) to tasks (e.g., jobs, routes). 

Built for real-world enterprise use cases, this solution supports:
- ✅ Streamlit-based user interface
- ✅ RESTful API for integration
- ✅ CLI & Docker support
- ✅ Notification integration (Slack/email ready)

---

## Problem Definition
The **Assignment Problem** seeks an optimal one-to-one mapping between agents and tasks based on a cost matrix, where:
- **Rows = Agents (e.g., employees)**
- **Columns = Tasks (e.g., jobs)**
- **Cell Value = Cost/Time of assigning agent to task**

Example:
```

|      | Job1 | Job2 | Job3 |
| ---- | ---- | ---- | ---- |
| Emp1 | 10   | 5    | 8    |
| Emp2 | 2    | 4    | 6    |
| Emp3 | 7    | 8    | 3    |

````

---

## How to Use

### Prediction Workflow
1. **Prepare your cost matrix** as a CSV file → `data/raw/cost_matrix.csv`
2. **Run the app or API** (see below)
3. **Get the optimized assignment**
4. **View or download the result** from `data/processed/assignment_result.csv`

---

## Run Locally (Streamlit Interface)

```bash
# Install dependencies
pip install -r requirements.txt

# Launch the Streamlit web app
streamlit run app/app.py
````

 Access it at: [http://localhost:8501](http://localhost:8501)

---

## Run as API Server (RESTful Endpoint)

```bash
# Install dependencies
pip install -r requirements.txt

# Run the FastAPI service
python src/api_service.py
```

 API Endpoint: [http://127.0.0.1:8000/predict](http://127.0.0.1:8000/predict)

###  Sample API Payload

```json
{
  "cost_matrix": [[10, 5, 8], [2, 4, 6], [7, 8, 3]]
}
```

---

## Run via Docker

```bash
docker build -t assignment-solver .
docker run -p 8501:8501 assignment-solver
```

---

## Project Modules & Logic

###  `app/app.py` – Streamlit Frontend

* Upload cost matrix
* Triggers Hungarian algorithm from backend
* Visualizes assignment and cost
* Downloads result as CSV

###  `src/model_training.py`

* Core logic for solving assignment problem using:

```python
from scipy.optimize import linear_sum_assignment
```

* Reads `cost_matrix.csv` and outputs `assignment_result.csv`

###  `src/api_service.py`

* Exposes REST API using FastAPI
* Accepts JSON input, returns optimal assignments + total cost

###  `src/notifier.py` *(Optional)*

* Placeholder for sending alerts via Slack/email

###  `notebooks/`

* `exploratory_analysis.ipynb`: Load & explore cost matrix
* `model_training_and_evaluation.ipynb`: Run Hungarian algo, visualize assignments

---

## Output Summary

| File                                   | Description                          |
| -------------------------------------- | ------------------------------------ |
| `data/processed/assignment_result.csv` | Optimal assignments + total cost     |
| `Streamlit UI`                         | View result matrix & download button |
| `API Response`                         | JSON with assignments and total cost |

---

## Project Structure

```
OR_assignment_problem_solver/
├── app/
│   └── app.py                     # Streamlit frontend
├── src/
│   ├── model_training.py          # Hungarian algorithm logic
│   ├── api_service.py             # FastAPI backend
│   └── notifier.py                # Optional alert system
├── data/
│   ├── raw/
│   │   └── cost_matrix.csv        # Input data
│   └── processed/
│       └── assignment_result.csv  # Output results
├── notebooks/
│   ├── exploratory_analysis.ipynb
│   └── model_training_and_evaluation.ipynb
├── requirements.txt
├── Dockerfile
└── README.md
```

---

## Real-World Use Cases

* Workforce management 🧑‍🏭
* Production line task assignment 🏭
* Logistics & delivery allocation 🚚
* Service scheduling (healthcare, field work) 🩺

---

## Future Extensions

* Slack or email notifications on job completion
* Support for unbalanced matrices
* Cost visualizations & heatmaps
* Batch processing of multiple matrices

---

### Built for operations research, logistics, and enterprise AI.

**Optimize intelligently. Deploy effortlessly.**

---
