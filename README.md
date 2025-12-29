# Reinforcement Learning Algorithms in Different Environments

This project is an **interactive web dashboard** built with **Flask + Vanilla JavaScript** to visualize how classical **Reinforcement Learning (RL)** algorithms behave in different environments.

It focuses on making **value functions, policies, and agent behavior** visible and intuitive for students and practitioners.

---

## 🌐 Live Demo

> [`http://127.0.0.1:5000/`](http://127.0.0.1:5000)

---

## 🖼️ Project Preview

<img width="1743" height="600" alt="image" src="https://github.com/user-attachments/assets/c47aa135-8d01-402b-9ae2-e73c3b5a5eff" />


<img width="1317" height="865" alt="image" src="https://github.com/user-attachments/assets/46283162-103a-4a85-9565-2485f621657c" />


---

## ✨ Features

### 🌍 Environments
- **GridWorldEnvironment**
  - Deterministic grid
  - Start, Goal, wall penalties
- **FrozenLakEnviroment**
  - Stochastic FrozenLake-style grid
  - Holes + slip probability

### 🧠 Algorithms
- Policy Evaluation
- Policy Improvement
- Policy Iteration
- Value Iteration
- Monte Carlo (Every-Visit & First-Visit)
- Temporal Difference **TD(0)**

### 📊 Visualizations
- Color-coded grid:
  - `S` – Start
  - `G` – Goal
  - `H` – Hole
  - `F` – Frozen / Free
- Policy arrows (↑ ↓ ← →)
- Animated agent movement
- Episode return plots (Chart.js)
- Tables for state values & rewards

### 🎛️ Interactive Parameters
- Grid size (rows, cols)
- Slip probability (FrozenLake)
- Discount factor `γ`
- Tolerance `θ`
- Episodes, learning rate `α`, exploration `ε`
- Stochastic simulation toggle
- Episode trace history

---

## 🧠 Algorithms

All algorithms share a **dictionary-based implementation style** for clarity:

```python
v[state]
Q[state][action]
policy[state]
```

### Dynamic Programming (Model-Based)

#### Policy Evaluation

```python
def policy_evaluation(givenPolicy, enviro, theta=0.0001, MAX=1000, gamma=0.9):
    v = {s: 0.0 for s in enviro.states}

    for _ in range(MAX):
        delta = 0.0
        for s in enviro.states:
            old_value = v[s]
            new_value = 0.0
            action = givenPolicy[s]

            for prob, next_state, reward in enviro.Prob[s][action]:
                new_value += prob * (reward + gamma * v[next_state])

            v[s] = new_value
            delta = max(delta, abs(new_value - old_value))

        if delta < theta:
            break

    return v
```

- Policy Improvement
- Policy Iteration (with history)
- Value Iteration (with optional trace)

---

### Monte Carlo (Model-Free)

Located in `Algorithms/Monte_CarloTypes.py`

- `monte_carlo_every_visit(...)`
- `monte_carlo_first_visit(...)`

Features:
- Episode generation
- Optional stochastic transitions
- Return tracking for learning curves

---

### Temporal Difference TD(0)

Located in `Algorithms/Temporal_Differance.py`

Update rule:

\[
Q(s,a) \leftarrow Q(s,a) + \alpha (r + \gamma \max_{a'} Q(s',a') - Q(s,a))
\]

Supports:
- ε-greedy exploration
- Episode return history

---

## 🌍 Environments

### 1️⃣ GridWorldEnvironment

- States: `(i, j)`
- Actions: `up, down, left, right`
- Deterministic transitions
- Rewards:
  - Wall → `-1`
  - Normal → `0`
  - Goal → `+10`

---

### 2️⃣ FrozenLakEnviroment

Extends GridWorld with:
- Random holes
- Slip probability
- Stochastic transitions
- Rewards:
  - Goal → `+10`
  - Hole / invalid → `-1`
  - Otherwise → `0`

---

## 🔌 Backend API (Flask)

### Routes

- `GET /`
- `GET /env/<env_name>`
- `GET /api/run_algorithm`
- `POST /api/simulate_policy`

Example response:

```json
{
  "policy": { "(i,j)": "action" },
  "values": { "(i,j)": 1.23 },
  "episode_returns": [],
  "trajectory": [],
  "env": "frozenlake",
  "rows": 4,
  "cols": 4
}
```

---

## 🎨 Frontend

### Tech Stack
- HTML + CSS
- Vanilla JavaScript
- Chart.js

### UI Components
- Environment selection cards
- Algorithm control panel
- Grid visualization
- Agent animation
- Value & reward tables
- Learning curves

---

## ⚙️ Running the App

### 1. Clone the repository

```bash
git clone https://github.com/Mariam-1611/Reinforcement_Learning_Algorithms_in_Different_Environment.git
cd Reinforcement_Learning_Algorithms_in_Different_Environment
```

### 2. Create virtual environment (optional)

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# Linux / Mac
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the server

```bash
python app.py
```

Open:

```
http://127.0.0.1:5000
```

---

## 🧪 Project Structure

```text
Reinforcement_Learning_Algorithms_in_Different_Environment/
│
├─ Algorithms/
│  ├─ Policy_Iteration.py
│  ├─ Value_Iteration.py
│  ├─ Monte_CarloTypes.py
│  └─ Temporal_Differance.py
│
├─ GridWorld_Enviroment.py
├─ FrozenLake_Enviroment.py
├─ app.py
├─ static/
│  ├─ style.css
│  └─ script.js
├─ templates/
│  ├─ index.html
│  └─ env_detail.html
├─ requirements.txt
└─ README.md
```

## 👩‍💻 Author

- **Name:** Mariam  
- **GitHub:** [@Mariam-1611](https://github.com/Mariam-1611)

---
