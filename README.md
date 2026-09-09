# FinVoyage

> **An intelligent personal finance agent that turns financial reality into better decisions.**

FinVoyage is an agentic personal finance system designed to understand a user's financial position, determine what they can safely spend, and make intelligent recommendations — starting with **travel planning**.

The long-term vision is to build a personal financial copilot capable of:

* Understanding bank and financial statements
* Categorizing and analyzing expenses
* Determining safe discretionary spending
* Planning affordable travel
* Detecting financial anomalies
* Identifying unnecessary expenses
* Suggesting investment opportunities
* Tracking financial goals
* Continuously improving financial decisions

---

## 🚀 Current Focus

The first version of FinVoyage will solve one problem exceptionally well:

> **"Given my current financial situation, what trip can I afford without compromising my financial goals?"**

The system will analyze financial data, calculate a safe travel budget, retrieve available travel options, and select the most suitable plan.

### Example

```text
Current Balance        ₹120,000
Expected Income        ₹80,000
Upcoming Expenses      ₹45,000
Emergency Reserve      ₹50,000
--------------------------------
Safe Discretionary     ₹25,000

Maximum Travel Budget  ₹18,000
```

The system can then evaluate:

```text
Goa             ₹17,000
Udaipur         ₹14,500
Mount Abu        ₹8,000
```

and recommend the option that provides the best combination of:

* Affordability
* Experience
* Duration
* Travel convenience
* User preferences
* Financial safety

---

# 🧠 Core Philosophy

FinVoyage should **not** equate:

```text
Bank Balance = Available Money
```

Instead:

```text
Financial Position
        ↓
Future Obligations
        ↓
Emergency Reserve
        ↓
Financial Goals
        ↓
Safe Discretionary Budget
        ↓
Travel Budget
        ↓
Travel Options
        ↓
Best Decision
```

The system should optimize for **financially responsible decisions**, not simply maximize spending.

---

# 🏗️ Initial Architecture

```text
                         ┌─────────────────────┐
                         │   Financial Sources  │
                         │                     │
                         │ Bank Statements     │
                         │ CSV / PDF           │
                         │ Manual Transactions │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ Transaction Engine  │
                         │                     │
                         │ Parse               │
                         │ Normalize           │
                         │ Categorize          │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │ Financial Analyzer  │
                         │                     │
                         │ Income              │
                         │ Expenses            │
                         │ Recurring expenses  │
                         │ Cash flow            │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Budget Engine     │
                         │                     │
                         │ Safe Balance        │
                         │ Emergency Reserve   │
                         │ Upcoming Expenses   │
                         │ Travel Budget       │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Travel Engine     │
                         │                     │
                         │ Search              │
                         │ Cost estimation     │
                         │ Itinerary           │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │  Decision Engine    │
                         │                     │
                         │ Filter              │
                         │ Score               │
                         │ Rank                │
                         │ Recommend           │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │    User / UI        │
                         │                     │
                         │ "Your best trip is  │
                         │  Goa for ₹17,000."  │
                         └─────────────────────┘
```

---

# 🎯 MVP

## Phase 1 — Financial Data

Support:

* CSV bank statements
* PDF bank statements
* Manual transactions

Extract:

```text
Date
Description
Debit
Credit
Balance
```

Normalize into:

```python
Transaction(
    date,
    description,
    amount,
    transaction_type,
    category,
    account
)
```

---

# Phase 2 — Expense Intelligence

Automatically categorize transactions.

Example:

```text
Swiggy          → Food
Uber            → Transport
Amazon          → Shopping
Netflix         → Subscription
Rent            → Housing
Salary          → Income
```

Calculate:

```text
Monthly Income
Monthly Expenses
Fixed Expenses
Variable Expenses
Discretionary Expenses
Recurring Expenses
Savings Rate
Current Cash Flow
```

---

# Phase 3 — Travel Budget

The system calculates a **Safe Travel Budget**.

Conceptually:

```text
Safe Balance
    =
Current Balance
- Upcoming Obligations
- Emergency Reserve
- Financial Goal Contributions
```

Then:

```text
Travel Budget
    =
Safe Discretionary Amount
× Travel Allocation
```

The exact formula should eventually become configurable rather than hard-coded.

---

# Phase 4 — Travel Recommendation

The Travel Engine receives:

```json
{
  "origin": "Ahmedabad",
  "budget": 18000,
  "duration": {
    "min": 3,
    "max": 5
  },
  "preferences": [
    "nature",
    "food",
    "relaxation"
  ]
}
```

It returns normalized travel plans:

```json
[
  {
    "destination": "Goa",
    "duration_days": 4,
    "estimated_cost": 17000,
    "transport_cost": 5000,
    "stay_cost": 6000,
    "food_cost": 3000,
    "activities_cost": 2000,
    "score": 0.91
  }
]
```

---

# 🏆 Travel Decision Engine

The decision engine should **not simply choose the cheapest trip**.

Each candidate should be evaluated across multiple dimensions.

Example:

```text
Affordability       30%
Experience          25%
User Preference     20%
Travel Convenience  10%
Duration             5%
Financial Safety    10%
```

Conceptually:

```python
score = (
    affordability_score * 0.30 +
    experience_score * 0.25 +
    preference_score * 0.20 +
    convenience_score * 0.10 +
    duration_score * 0.05 +
    financial_safety_score * 0.10
)
```

These weights should eventually be configurable.

---

# 🤖 Agentic Architecture

AI should be introduced where reasoning is valuable.

Do **not** use an LLM for deterministic financial calculations.

### Deterministic

```text
Transaction parsing
Expense aggregation
Balance calculations
Budget calculations
Financial constraints
Cost calculations
```

### AI-assisted

```text
Transaction categorization
Merchant interpretation
Travel preference understanding
Travel-plan comparison
Natural-language explanations
Financial insights
```

Eventually the system can be orchestrated using LangGraph:

```text
                  ┌───────────────┐
                  │ Financial     │
                  │ Agent         │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ Budget        │
                  │ Agent         │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ Travel        │
                  │ Agent         │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ Decision      │
                  │ Agent         │
                  └───────┬───────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ Recommendation│
                  └───────────────┘
```

---

# 🛠️ Proposed Technology Stack

## Backend

```text
Python
FastAPI
PostgreSQL
SQLAlchemy
Pydantic
```

## Data Processing

```text
Pandas
PyMuPDF / pdfplumber
```

## AI

```text
LangChain
LangGraph
LLM provider abstraction
```

## Frontend

```text
Next.js
TypeScript
Tailwind CSS
```

## Infrastructure

```text
Docker
PostgreSQL
Redis (later)
```

---

# 📁 Initial Repository Structure

```text
finvoyage/
│
├── README.md
├── LICENSE
├── .gitignore
├── docker-compose.yml
│
├── docs/
│   ├── vision.md
│   ├── architecture.md
│   └── decisions/
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── domain/
│   │   │   ├── transactions/
│   │   │   ├── finance/
│   │   │   ├── budget/
│   │   │   └── travel/
│   │   │
│   │   ├── application/
│   │   ├── infrastructure/
│   │   └── main.py
│   │
│   └── tests/
│
├── frontend/
│   └── ...
│
└── scripts/
    └── import_statement.py
```

---

# 🧩 Domain Boundaries

Keep these domains independent from the beginning:

```text
Transaction
     │
     ▼
Financial Analysis
     │
     ▼
Budget
     │
     ▼
Travel
     │
     ▼
Decision
```

This will make it possible to later add:

```text
Investment
Expense Optimization
Anomaly Detection
Financial Goals
Net Worth
Subscriptions
Tax Planning
```

without turning the application into a monolith of business logic.

---

# 🔐 Privacy & Security

Financial data is highly sensitive.

Initial development should use:

```text
Local PostgreSQL
Local statement uploads
Encrypted secrets
No production bank credentials
No direct bank access
```

Never send raw bank statements to an LLM unless absolutely necessary.

Prefer:

```text
Bank Statement
      ↓
Local Parser
      ↓
Normalized Transactions
      ↓
Redacted / Minimal Data
      ↓
LLM
```

The financial calculation layer should remain deterministic and auditable.

---

# 🧪 First End-to-End Goal

The first working version should be able to execute:

```text
Upload bank statement

        ↓

Extract transactions

        ↓

Categorize transactions

        ↓

Calculate current month's
financial position

        ↓

Calculate safe travel budget

        ↓

Fetch travel options

        ↓

Filter options exceeding budget

        ↓

Rank remaining options

        ↓

Recommend the best trip

        ↓

Explain why
```

Example final response:

```text
You can safely allocate ₹18,000 for travel this month.

Recommended trip:
Goa — 4 days

Estimated cost:
₹17,000

Why:
• Fits within your travel budget
• Leaves ₹1,000 buffer
• Good match for your preferences
• Strong experience-to-cost ratio

Financial impact:
₹18,000 budget
₹17,000 estimated spend
₹1,000 remaining travel buffer
```

---

# 🗺️ Roadmap

### v0.1 — Financial Import

* [ ] CSV import
* [ ] PDF statement parser
* [ ] Transaction model
* [ ] Transaction categorization
* [ ] Monthly aggregation

### v0.2 — Budget Engine

* [ ] Income detection
* [ ] Recurring expense detection
* [ ] Upcoming expense estimation
* [ ] Emergency reserve
* [ ] Safe discretionary budget
* [ ] Travel budget

### v0.3 — Travel Engine

* [ ] Travel provider integration
* [ ] Destination search
* [ ] Cost normalization
* [ ] Itinerary representation

### v0.4 — Decision Engine

* [ ] Travel constraints
* [ ] Candidate filtering
* [ ] Scoring
* [ ] Ranking
* [ ] Recommendation explanation

### v0.5 — Agentic Layer

* [ ] LangGraph workflow
* [ ] Financial analysis agent
* [ ] Travel research agent
* [ ] Recommendation agent
* [ ] Human approval step

### v1.0 — Personal Financial Copilot

* [ ] Anomaly detection
* [ ] Expense optimization
* [ ] Investment suggestions
* [ ] Financial goals
* [ ] Net-worth tracking
* [ ] Automated financial reports

---

# 💡 Long-Term Vision

FinVoyage should eventually answer questions such as:

> "Can I afford Vietnam in December?"

> "How much can I spend on my birthday?"

> "Why did I spend 20% more this month?"

> "Where am I wasting money?"

> "Can I buy a Mac this year without delaying my investment goals?"

> "What is the best trip I can take with ₹30,000?"

> "What should I do with my surplus this month?"

The ultimate goal is not a travel planner.

It is a **decision engine for personal finance**.

```text
              MONEY
                │
                ▼
        ┌───────────────┐
        │   FINVOYAGE   │
        └───────┬───────┘
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
    SPEND     TRAVEL   INVEST
       │        │        │
       └────────┼────────┘
                ▼
        BETTER DECISIONS
```

---

## License

To be decided.
