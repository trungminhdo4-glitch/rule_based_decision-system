# rule_based_decision-system

Rule-Based Adaptive Decision System

A modular, explainable, rule-based decision engine with adaptive behavior.
The system evaluates data points using multiple rules, aggregates weighted scores, produces decisions, and continuously adapts based on historical performance.

🚀 Motivation

This project explores how transparent rule-based systems can be combined with adaptive mechanisms to create decision engines that are:

explainable (no black box)

modular and extensible

dynamically improving over time

The focus is on clarity, structure, and learning from past decisions, not on machine learning models.

🧠 Core Concepts
1. Rules

Each rule evaluates one aspect of the input data and returns a score:

ValueRule → evaluates value strength

RiskRule → evaluates downside risk

VolatilityRule → evaluates stability

Scores:

+1.0 → positive

0.0 → neutral / missing data

-1.0 → negative

2. Weighted Aggregation

Each rule has a weight.
Final score = sum of (rule_score × rule_weight)

3. Decision Logic

Based on the total score:

ACCEPT → score ≥ accept threshold

REJECT → score ≤ reject threshold

HOLD → otherwise

Thresholds adapt over time.

4. Explainability

Every decision includes:

rule name

raw score

weight

weighted contribution

human-readable reason

5. Adaptivity

The system adapts using historical performance:

rule weights (EMA-based)

rule parameters (e.g. min_value, max_risk)

decision thresholds (based on HOLD frequency)


▶️ How to Run
python main.py


Optional (recommended):

python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
python main.py

📊 Example Output
--- Data Point 1 ---
ValueRule: raw=-1.0, weight=0.33 → weighted=-0.33
RiskRule: raw=-1.0, weight=0.33 → weighted=-0.33
VolatilityRule: raw=0.0, weight=0.33 → weighted=0.00

Total Score: -0.66
Decision: REJECT

Explanation:
- ValueRule: value=40 < min_value=60
- RiskRule: risk=0.6 > max_risk=0.3
- VolatilityRule: volatility missing or invalid



rule_based_decision_system/
│
├─ core/
│   ├─ rules/
│   │   ├─ base_rule.py
│   │   ├─ value_rule.py
│   │   ├─ risk_rule.py
│   │   └─ volatility_rule.py
│   │                                           
│   ├─ rule_engine.py
│   ├─ decision.py
│   └─ __init__.py
│
├─ evaluation/
│   ├─ adaptive.py          ← EIN Adaptive-System
│   ├─ scorer.py
│   ├─ explanation.py
│   ├─ history.py
│   └─ __init__.py
│
├─ data/
│   └─ input_data.py
│
├─ app_logging/
│   └─ logger.py
│
├─ main.py
├─ requirements.txt
├─ README.md
└─ .gitignore
