# Synapse-OPS

> A policy-aware, tool-using AI agent for automated incident resolution in food delivery operations.

Synapse-OPS is an intelligent agent prototype designed to handle operational disruptions for platforms like GrabFood and GrabMart. It uses a Large Language Model (LLM) orchestrated via LangChain/LangGraph to reason through incidents, query deterministic tools, apply business policies, and resolve issues like merchant backlogs, missing items, or driver breakdowns.

## 🚀 Features

* **Autonomic Reasoning:** Uses Chain-of-Thought (CoT) to plan and execute resolution steps.
* **Policy Compliance:** strictly adheres to `policies.json` (e.g., refund caps, verification rules) before taking action.
* **Deterministic Tooling:** Includes a suite of simulated, deterministic APIs (`tools.py`) for consistent testing and demonstration.
* **Incident Classification:** ML-based router (`router.py`) to categorize incoming tickets (e.g., `merchant_backlog`, `packaging_issue`).
* **Auditable Logs:** Saves full decision traces to `logs/` in structured JSON format for review.

## 🛠️ Components

The system is built with **Python 3.x** and **LangGraph**.

| Component | Description |
|-----------|-------------|
| `reasoner.py` | The main agent orchestrator using LangGraph to manage state and tool calls. |
| `tools.py` | A deterministic API layer simulating merchant status, driver assignment, and refund logic. |
| `policies.json` | Configurable business rules (e.g., auto-refund limits, allowed rerouting merchants). |
| `router.py` | Logistic Regression classifier (TF-IDF) to route raw descriptions to incident types. |
| `run_demo.py` | CLI batch runner to process scenarios from `scenarios.json`. |

## 📦 Installation

1.  **Clone the repository**
    ```bash
    git clone https://github.com/toad-of-code/synapse-ops.git
    cd synapse-ops
    ```

2.  **Install Dependencies**
    *(Note: Ensure you have Python 3.9+)*
    ```bash
    pip install langchain langgraph langchain-mistralai pydantic pandas scikit-learn python-dotenv nest_asyncio
    ```

3.  **Environment Setup**
    Create a `.env` file in the root directory and add your LLM API key (the project defaults to Mistral, but can be adapted):
    ```bash
    MISTRAL_API_KEY=your_api_key_here
    ```

## 💻 Usage

### Run the Demo
To run the standard batch of scenarios defined in `scenarios.json`:

```bash
python run_demo.py

```

This will:

1. Load scenarios.
2. Initialize the agent.
3. Process each incident step-by-step.
4. Print the reasoning traces and final outcomes.
5. Save detailed logs to the `logs/` directory.

### Run Custom Scenarios

You can create a custom JSON file with new scenarios and run it:

```bash
python run_demo.py -s my_custom_scenarios.json

```

### Retrain the Classifier

If you update `sample_train_data.csv`, you can retrain the incident router:

```bash
python router.py --retrain

```

## 📊 Project Structure

```text
synapse-ops/
├── logs/                   # Generated decision traces (JSON)
├── tools.py                # Simulated API tools
├── reasoner.py             # Agent logic & graph definition
├── router.py               # ML Incident Classifier
├── run_demo.py             # Main entry point script
├── policies.json           # Dynamic policy configuration
├── scenarios.json          # Test cases
├── sample_train_data.csv   # Training data for router
├── decision_trace.py       # Pydantic schemas for logging
└── BUILD_NOTES.md          # Development tracker

```

## 🛡️ Policy Engine

The agent's behavior is governed by `policies.json`. You can modify this file to test different outcomes without changing code.

**Example Policy Config:**

```json
{
  "auto_refund_max_amount": 500,
  "refund_percent_cap": 25,
  "escalation_rules": {
    "customer_unreachable": true
  }
}

```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the project.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes.
4. Push to the branch.
5. Open a Pull Request.

## 📝 License

Distributed under the MIT License. See `LICENSE` for more information.

## 📧 Contact

Project Link: [https://github.com/toad-of-code/synapse-ops](https://www.google.com/search?q=https://github.com/toad-of-code/synapse-ops)

```
