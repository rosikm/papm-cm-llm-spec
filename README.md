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

## ✅ What's Inside

- **Function Registry**: All PAPM functions with signatures, types, examples, and retrieval metadata.
- **Grammar**: EBNF + operator precedence for parsing and validation.
- **Contexts**: Calculation contexts for grouping and scoping.
- **Data Types & Constants**: Supported types and built-in constants.
- **Vocabulary Template**: Map user terms to dataset columns.
- **Examples**: Few-shot pairs for training or prompting.
- **Policies**: Guardrails for validation, canonicalization, and type safety.

---

## ⚠️ Important Syntax Notes

**Logical Operators**: PAPM uses **symbolic operators only**:

- ✅ Use `&&` for logical AND
- ✅ Use `||` for logical OR  
- ✅ Use `!` for logical NOT
- ❌ Word-based operators (`AND`, `OR`, `NOT`) are **NOT supported**

**Attribute References**:

- ✅ Simple names (no spaces): Use directly as identifiers → `userName`, `Activity`, `InvoiceAmount`
- ❌ Do NOT use brackets for simple names → `[userName]`, `[Activity]` are **INVALID**
- ✅ Names with spaces: Use `GETVALUE()` function → `GETVALUE("invoice total")`
- ❌ Do NOT use brackets for any attribute names → `[invoice total]` is **INVALID**

See `policies/guardrails.json` and `policies/canonicalization.json` for complete syntax rules.

---

## ✅ How to Use

1. **Index the registry** for RAG or embedding-based retrieval.
2. **Load grammar and policies** for formula validation and canonicalization.
3. **Inject few-shot examples** into your LLM prompt for better accuracy.
4. **Provide vocabulary mapping** at runtime for schema alignment.
5. **Validate outputs** using grammar + type rules before execution.

---

## ✅ Quickstart Guide

### VS Code

Use this repository with **GitHub Copilot Chat in Agent Mode** to get AI assistance for PAPM formula generation:

#### Getting Started

1. **Open from GitHub**:
   - In VS Code, press `Ctrl/Cmd + Shift + P` to open the Command Palette
   - Type and select **"Git: Clone"**
   - Enter the repository URL: `https://github.com/rosikm/papm-cm-llm-spec.git`
   - Choose a local folder and open the repository

2. **Enable GitHub Copilot Agent Mode**:
   - Open GitHub Copilot Chat panel (click the chat icon in the sidebar or press `Ctrl/Cmd + Shift + I`)
   - Type `@workspace` in the chat to enable agent mode with workspace context
   - The agent now has access to all specification files in this repository

#### Using Copilot Agent Mode

With agent mode enabled, GitHub Copilot can intelligently search and reference files from this specification. Example prompts:

**Ask for formula help**:

```text
@workspace How do I write a formula to count cases where invoice amount exceeds 10000 per country?
```

**Request syntax guidance**:

```text
@workspace What's the correct syntax for calculating average duration per activity?
```

**Learn about functions**:

```text
@workspace Show me all aggregation functions available in PAPM and give examples
```

**Validate formulas**:

```text
@workspace Check if this formula is correct: [userName] == "John" AND Activity == "Review"
```

**Get examples**:

```text
@workspace Show me examples using the GETVALUE function for attributes with spaces
```

**Understand attribute references**:

```text
@workspace How do I reference attributes with spaces in their names?
```

#### Tips for Best Results

- **Always use `@workspace`** to activate agent mode and workspace context
- **Be specific** about your data schema (mention attribute names and types)
- **Provide context** about what you're trying to calculate or analyze
- **Ask for validation** when unsure about syntax
- **Reference examples** by asking Copilot to show similar patterns from the spec
- The agent will automatically search through `functions/registry.jsonl`, `examples/prompts_to_formulas.jsonl`, and policy files

### Claude Desktop

Use this repository with **Claude Desktop** for formula generation assistance by adding it directly from GitHub:

#### Setup Instructions

1. **Open Claude Desktop**

2. **Add this repository from GitHub**:
   - Click the **+ icon** in the Claude Desktop interface
   - Select **"Add from GitHub"**
   - Enter the repository URL: `https://github.com/rosikm/papm-cm-llm-spec`
   - Click **Add** to integrate the repository

3. **Verify integration**:
   - You should see the repository listed in your Projects
   - Claude now has access to all specification files

#### Using the Specification

Once added, Claude has access to all specification files. Example prompts:

**Ask for formula help**:

```text
Can you read the PAPM function registry and help me write a formula 
to calculate the average invoice amount per vendor?
```

**Request examples**:

```text
Show me examples from prompts_to_formulas.jsonl that demonstrate 
how to use the COUNTIF function
```

**Validate syntax**:

```text
Check the policies/guardrails.json file and tell me if this formula 
follows the correct syntax: [userName] == "John" AND Activity == "Review"
```

**Explore functions**:

```text
Read functions/registry.jsonl and list all aggregation functions 
available in PAPM
```

**Learn syntax rules**:

```text
What are the attribute reference rules according to 
policies/canonicalization.json?
```

#### Best Practices

- **Reference specific files** when asking questions for more accurate responses
- **Provide your data schema** (column names, types) for context-aware formulas
- **Ask for validation** by referencing `policies/guardrails.json`
- **Request examples** from `examples/prompts_to_formulas.jsonl` to see patterns
- **Start conversations** in the project context for automatic access to all spec files

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

## ✅ Feedback

Any feedback, successes or failures are [more than welcome](mailto:michal.rosik@microsoft.com).

---

## ✅ License

LICENSE (or your preferred license)
