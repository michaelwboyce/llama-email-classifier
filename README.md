# Llama Email Classifier

A local AI email-classification project that uses TinyLlama through `llama-cpp-python` to sort incoming messages into three practical inbox categories: **Priority**, **Updates**, and **Promotions**.

## Project Overview

The goal of this project is to build a lightweight email assistant that can identify which messages require immediate attention, which are informational updates, and which are promotional content.

The classifier combines:

- a locally loaded GGUF language model
- few-shot prompt engineering
- deterministic generation settings
- a small rule-based guardrail for obvious promotional language

## Classification Categories

| Category | Description |
| --- | --- |
| **Priority** | Important or time-sensitive messages that require action or could cause a negative consequence if ignored |
| **Updates** | Informational messages about an ongoing project, order, thread, or status that do not require immediate action |
| **Promotions** | Advertising, sales, discounts, coupons, special offers, or shopping-related messages |

## Model

This project uses:

- **TinyLlama 1.1B Chat**
- GGUF quantized model
- `llama-cpp-python==0.2.82`

The notebook downloads the model from Hugging Face at runtime rather than storing the large `.gguf` file in the repository.

## Approach

The project follows four main steps:

1. Load the email dataset with pandas.
2. Initialize the local TinyLlama model.
3. Build a few-shot classification prompt with examples for each category.
4. Classify emails with a `process_message()` function.

Because the small local model occasionally confused promotional language with urgent language, the final solution also adds a lightweight keyword guardrail for obvious promotion terms such as `sale`, `discount`, `% off`, `coupon`, and `special offer`.

This illustrates a practical hybrid AI pattern: **LLM + deterministic business rules**.

## Repository Structure

```text
llama-email-classifier/
├── llama_email_classifier.ipynb
├── data/
│   ├── email_categories_data.csv
│   └── models.csv
├── requirements.txt
├── .gitignore
└── README.md
```

## Setup

Clone the repository and install the required packages:

```bash
pip install -r requirements.txt
```

The notebook contains a command that downloads the TinyLlama GGUF model automatically.

## Example Output

For the first two dataset examples, the completed classifier returns:

```text
Email 1: Priority
Email 2: Promotions
```

## Skills Demonstrated

- Python
- pandas
- local LLM inference
- prompt engineering
- few-shot classification
- response parsing
- deterministic generation settings
- hybrid AI / rule-based guardrails
- Jupyter notebooks

## Key Takeaway

Small language models can be useful for lightweight local classification, but they may need stronger prompts or deterministic guardrails for edge cases. Combining LLM inference with simple rules can improve reliability while keeping the system interpretable.

## Notes

The `model.gguf` file is intentionally excluded from version control because model files are large. The notebook downloads the model when needed.
