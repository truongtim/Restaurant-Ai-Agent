# Secure Multi-Agent Restaurant Intelligence System

A multi-agent AI pipeline that analyzes restaurant reviews and computes an overall quality score on a 0-10 scale. Built using Microsoft AutoGen and OpenAI GPT-4o-mini for CSCI 5240 - Generative AI.

## Overview

This system processes a natural language restaurant query through a sequential pipeline of four specialized AI agents. Each agent has a distinct role and passes its output to the next agent in the chain. The pipeline also includes LLM security features to detect and block adversarial prompt injection attacks.

## Pipeline Architecture

```
User Query
    |
Security Agent        - Validates the query for adversarial content
    |
Data Fetch Agent      - Retrieves all reviews for the restaurant from the dataset
    |
Review Analysis Agent - Extracts food and customer service scores from each review
    |
Scoring Agent         - Computes the final weighted score using a mathematical formula
```

## Agents

**Security Agent** - Inspects the incoming query and outputs either SAFE or BLOCKED. If blocked, the pipeline halts immediately.

**Data Fetch Agent** - Calls fetch_restaurant_data() to retrieve all reviews for the queried restaurant from restaurant-data.txt.

**Review Analysis Agent** - Scans each review for scoring keywords and assigns a food score and customer service score (1-5) per review based on the following table:

| Score | Keywords |
|-------|----------|
| 1 | awful, horrible, disgusting |
| 2 | bad, unpleasant, offensive |
| 3 | average, uninspiring, forgettable |
| 4 | good, enjoyable, satisfying |
| 5 | awesome, incredible, amazing |

**Scoring Agent** - Calls calculate_overall_score() using the extracted scores to produce a final score.

## Scoring Formula

```
score = (10 / (N * sqrt(125))) * SUM( sqrt(food[i]^2 * service[i]) )
```

Where food[i] and service[i] are the scores for review i, and N is the total number of reviews.

## Setup

```bash
# Create and activate virtual environment
python -m venv venv
venv\Scripts\activate

# Install dependencies
pip install pyautogen openai

# Set OpenAI API key
$env:OPENAI_API_KEY="your-key-here"
```

## Usage

```bash
python Student.py "How good is Subway?"
python Student.py "What is the overall score for Taco Bell?"
```

## Testing

```bash
python test.py
```

## File Structure

```
Assignment1/
├── Student.py           - Main implementation
├── restaurant-data.txt  - Dataset of restaurant reviews
├── attack-1.txt         - Basic prompt injection attack prompt
├── attack-2.txt         - Sophisticated prompt injection attack prompt
├── defense.txt          - Defense prompt and Security Agent system message
├── test.py              - Public test script
└── requirements.txt     - Dependencies
```

## Built With

- AutoGen - Multi-agent orchestration framework
- OpenAI GPT-4o-mini - Large language model
- Python 3.11

## Author

Tim Truong - CSCI 5240 Generative AI
