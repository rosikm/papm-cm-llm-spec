# PAPM CM LLM-Ready Documentation Package

This repository provides a **machine-readable specification** for **Power Automate Process Mining (PAPM) custom metrics**, designed to enable an **LLM-based agent** to translate natural language into syntactically correct PAPM formulas.

---

## 📂 Repository Structure

```ultree
papm-llm-spec/
├── functions/
│   ├── function.schema.json            # JSON schema for function entries
│   └── registry.jsonl                  # All PAPM functions in JSONL format
├── grammar/
│   ├── expression.ebnf                 # EBNF grammar for PAPM formulas
│   └── operators.json                  # Operator precedence & type rules
├── contexts/
│   └── calculation-contexts.json       # Supported calculation contexts
├── types/
│   ├── data-types.json                 # INT, FLOAT, DATE, TIME, etc.
│   └── constants.json                  # PI, E constants
├── vocabulary/
│   └── eventlog.columns.template.jsonl # Template for schema synonyms
├── examples/
│   └── prompts_to_formulas.jsonl       # Few-shot NL → formula examples
├── policies/
│   ├── typing_nulls_time.json          # Type coercion & null handling
│   ├── canonicalization.json           # Formatting rules for formulas
│   └── guardrails.json                 # Safety & validation rules
└── README.md
```
---

## ✅ What’s Inside

- **Function Registry**: All PAPM functions with signatures, types, examples, and retrieval metadata.
- **Grammar**: EBNF + operator precedence for parsing and validation.
- **Contexts**: Calculation contexts for grouping and scoping.
- **Data Types & Constants**: Supported types and built-in constants.
- **Vocabulary Template**: Map user terms to dataset columns.
- **Examples**: Few-shot pairs for training or prompting.
- **Policies**: Guardrails for validation, canonicalization, and type safety.

---

## ✅ How to Use

1. **Index the registry** for RAG or embedding-based retrieval.
2. **Load grammar and policies** for formula validation and canonicalization.
3. **Inject few-shot examples** into your LLM prompt for better accuracy.
4. **Provide vocabulary mapping** at runtime for schema alignment.
5. **Validate outputs** using grammar + type rules before execution.

---

## ✅ Sources

All function definitions and rules are based on official Microsoft Learn documentation:

- [Custom Metrics Overview](https://learn.microsoft.com/en-us/power-automate/minit/custom-metrics)
- [Aggregations](https://learn.microsoft.com/en-us/power-automate/minit/aggregations)
- [Date & Time Operations](https://learn.microsoft.com/en-us/power-automate/minit/date-and-time-operations)
- [Statistical Operations](https://learn.microsoft.com/en-us/power-automate/minit/statistical-operations)
- [String Operations](https://learn.microsoft.com/en-us/power-automate/minit/string-operations)
- [Other Operations](https://learn.microsoft.com/en-us/power-automate/minit/other-operations)
- [Unary/Binary Operators](https://learn.microsoft.com/en-us/power-automate/minit/unary-operators)
- [Calculation Context](https://learn.microsoft.com/en-us/power-automate/minit/calculation-context)
- [Data Types](https://learn.microsoft.com/en-us/power-automate/minit/data-types-custom-metrics)
- [Constants](https://learn.microsoft.com/en-us/power-automate/minit/constants)

---

## ✅ Contribution Guidelines

- Validate JSON files against `function.schema.json` before committing.
- Keep JSONL entries ≤ 1.2K tokens for efficient chunking.
- Add new examples to `examples/prompts_to_formulas.jsonl` with rationale.
- Follow canonicalization rules in `policies/canonicalization.json`.

---

## ✅ License

LICENSE (or your preferred license)
