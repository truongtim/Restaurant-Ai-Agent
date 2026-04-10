# 🍽️ Secure Multi-Agent Restaurant Intelligence System

A multi-agent AI pipeline that analyzes restaurant reviews and computes quality scores, built with AutoGen and OpenAI. Developed for CSCI 5240 - Generative AI.

---

## 📋 Overview

This system uses four AI agents working together in a pipeline to:
1. Validate incoming queries for security threats
2. Fetch restaurant reviews from a dataset
3. Analyze each review and extract food and service scores
4. Compute a final weighted score for the restaurant

---

## 🏗️ System Architecture

```
User Query
    ↓
Security Agent      → Checks if query is safe or adversarial
    ↓
Data Fetch Agent    → Retrieves all reviews for the restaurant
    ↓
Review Analysis Agent → Scores each review (food + customer service)
    ↓
Scoring Agent       → Computes final weighted score (0-10)
```

---

## 🤖 Agents

| Agent | Role |
|-------|------|
| **Security Agent** | Inspects queries for prompt injection or adversarial content. Outputs `SAFE: <query>` or `BLOCKED: <reason>` |
| **Data Fetch Agent** | Calls `fetch_restaurant_data()` to retrieve reviews from the dataset |
| **Review Analysis Agent** | Maps keywords to scores (1-5) for food and customer service |
| **Scoring Agent** | Calls `calculate_overall_score()` to compute the final score |

---

## 📊 Scoring Formula

$$\text{score} = \frac{10}{N \cdot \sqrt{125}} \sum_{i=1}^{N} \sqrt{f_i^2 \cdot c_i}$$

Where:
- $f_i$ = food score for review $i$
- $c_i$ = customer service score for review $i$
- $N$ = total number of reviews

---

## 🔑 Keyword Scoring

| Score | Keywords |
|-------|----------|
| 1 | awful, horrible, disgusting |
| 2 | bad, unpleasant, offensive |
| 3 | average, uninspiring, forgettable |
| 4 | good, enjoyable, satisfying |
| 5 | awesome, incredible, amazing |

---

## 🔒 Security Features

- **Security Agent** blocks adversarial queries before they enter the pipeline
- **Defense prompt** prevents secret key leakage from LLM systems
- Handles prompt injection, virtualization, and obfuscation attacks

---

## 🚀 Setup & Installation

### Prerequisites
- Python 3.11+
- OpenAI API key with credits

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR-USERNAME/restaurant-ai-agent.git
cd restaurant-ai-agent

# Create and activate virtual environment
python -m venv venv
venv\Scripts\activate  # Windows
source venv/bin/activate  # Mac/Linux

# Install dependencies
pip install pyautogen openai

# Set your OpenAI API key
$env:OPENAI_API_KEY="sk-your-key-here"  # Windows PowerShell
export OPENAI_API_KEY="sk-your-key-here"  # Mac/Linux
```

---

## 💻 Usage

```bash
python Student.py "How good is Subway?"
python Student.py "What is the overall score for Taco Bell?"
python Student.py "How good is Krispy Kreme?"
```

### Example Output
```
The final overall score for Subway is 7.066.
```

---

## 🧪 Testing

```bash
python test.py
```

---

## 📁 File Structure

```
Assignment1/
├── Student.py          # Main implementation
├── restaurant-data.txt # Dataset of restaurant reviews
├── attack-1.txt        # Basic prompt injection attack
├── attack-2.txt        # Sophisticated prompt injection attack
├── defense.txt         # Defense prompt + Security Agent prompt
├── test.py             # Public test script
└── requirements.txt    # Dependencies
```

---

## 🛠️ Built With

- [AutoGen](https://github.com/microsoft/autogen) - Multi-agent orchestration framework
- [OpenAI GPT-4o-mini](https://openai.com) - Language model
- Python 3.11

---

## 👤 Author

**Tim Truong**  
CSCI 5240 - Generative AI
