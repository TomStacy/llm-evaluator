# LLM Evaluator

A Python project for evaluating Large Language Models (LLMs) using the uv package manager.

## Features

- Python scripts for LLM evaluation
- Jupyter notebooks for interactive analysis
- Modern Python development with uv package manager
- Git version control

## Prerequisites

- Python 3.10 or higher
- [uv](https://github.com/astral-sh/uv) package manager
- Git

## Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd llm-evaluator
```

### 2. Install Dependencies

```bash
uv sync
```

This will create a virtual environment and install all required packages:

- Jupyter for interactive notebooks
- pandas for data manipulation
- requests for API calls
- beautifulsoup4 for web scraping
- playwright for browser automation
- openai for OpenRouter API client

### 3. Install Playwright Browsers (One-Time Setup)

The notebook uses Playwright to scrape the OpenRouter rankings page. Install the required browser:

```bash
uv run playwright install chromium
```

### 4. Get Your OpenRouter API Key

1. Sign up for a free account at [OpenRouter](https://openrouter.ai/)
2. Generate an API key from your dashboard
3. Set it as an environment variable:

**Windows (PowerShell):**

```powershell
$env:OPENROUTER_API_KEY="your-api-key-here"
```

**Mac/Linux (Bash/Zsh):**

```bash
export OPENROUTER_API_KEY="your-api-key-here"
```

**Alternative: Create a `.env` file** (for persistent storage):

```bash
echo "OPENROUTER_API_KEY=your-api-key-here" > .env
```

### 5. Start Using the Notebook

Open the notebook and start evaluating models:

```bash
uv run jupyter notebook notebooks/llm-compare.ipynb
```

Or open it directly in VS Code with the Jupyter extension.

## Project Structure

```text
llm-evaluator/
├── .github/
│   └── copilot-instructions.md  # Copilot configuration
├── notebooks/                    # Jupyter notebooks
│   └── llm-compare.ipynb        # LLM comparison notebook
├── .gitignore                   # Git ignore rules
├── .python-version              # Python version specification
├── pyproject.toml              # Project configuration
├── README.md                   # This file
└── uv.lock                     # Locked dependencies
```

## Usage

### Running the LLM Comparison Notebook

The main notebook (`notebooks/llm-compare.ipynb`) performs a comprehensive evaluation of language models:

1. **Start Jupyter:**

   ```bash
   uv run jupyter notebook
   ```

   Then navigate to `notebooks/` and open `llm-compare.ipynb`

2. **Or open directly in VS Code:**

   - Install the Jupyter extension for VS Code
   - Open `notebooks/llm-compare.ipynb`
   - Click "Select Kernel" → "Python Environments" → Choose the uv environment

### What the Notebook Does

1. **Fetches Top Models** - Scrapes current rankings from OpenRouter
2. **Generates Questions** - Each model creates a challenging reasoning question
3. **Answers Questions** - Each model answers all questions
4. **Evaluates Responses** - Each model rates all answers on a 10-point scale
5. **Produces Results** - Generates comparison metrics and rating matrices

### Customization

You can modify the notebook to:

- Change the number of models evaluated (default: top 5)
- Use different sorting criteria (`popularity`, `price_low`, `price_high`, `context_length`, `newest`)
- Adjust evaluation prompts and rating criteria
- Export results to different formats

## Code Quality

This project leverages a dual-tool approach to ensure high code quality and maintainability:

### 🦀 Ruff - Lightning-Fast Linting & Formatting

[Ruff](https://github.com/astral-sh/ruff) is an extremely fast Python linter and formatter written in Rust, providing:

- **Style Enforcement**: Catches PEP 8 violations, naming conventions, and code smells
- **Auto-fixing**: Automatically corrects many issues (import sorting, formatting, etc.)
- **Modern Python**: Enforces best practices and suggests upgrades to modern Python idioms
- **Comprehensive Rules**: Includes checks from pylint, flake8, isort, pyupgrade, and more

**Running Ruff:**

```bash
# Check for linting issues
uv run ruff check .

# Format code
uv run ruff format .

# Fix auto-fixable issues
uv run ruff check --fix .
```

### 🔍 Pyright - Advanced Type Checking

[Pyright](https://github.com/microsoft/pyright) (via Pylance in VS Code) provides static type analysis:

- **Type Safety**: Catches type-related bugs before runtime
- **IDE Integration**: Powers IntelliSense, auto-completion, and inline documentation
- **Gradual Typing**: Works with both typed and untyped code
- **Performance**: Fast analysis even on large codebases

### Notebook-Friendly Configuration

Both tools are configured to work seamlessly with Jupyter notebooks:

- **Relaxed Line Length**: 120 characters (accommodates longer docstrings)
- **Import Flexibility**: Disabled import sorting for notebooks (cells execute non-linearly)
- **Type Checking**: Set to "off" for notebooks to prevent false positives with dynamic types
- **Smart Ignores**: Whitespace and line length rules relaxed for notebook cells

This configuration is defined in:

- `pyproject.toml` - Ruff settings
- `pyrightconfig.json` - Pyright configuration
- `.vscode/settings.json` - VS Code workspace settings

**Why Both Tools?**

Ruff and Pyright complement each other:

- **Ruff** focuses on code style, common errors, and best practices
- **Pyright** focuses on type correctness and provides rich IDE features

Together, they create a comprehensive quality gate that catches issues early while remaining fast and developer-friendly, especially in the mixed environment of scripts and interactive notebooks.

## Development

### Adding New Dependencies

```bash
uv add <package-name>
```

### Adding Development Dependencies

```bash
uv add --dev <package-name>
```

### Updating Dependencies

```bash
uv sync
```

## Contributing

1. Create a feature branch
1. Make your changes
1. Submit a pull request

## Evaluation Results

### LLM Model Comparison (OpenRouter Rankings)

This evaluation compares the top 5 models from OpenRouter by having each model:

1. Generate a challenging reasoning question
2. Answer all questions from other models
3. Rate the quality of all answers on a 10-point scale

#### Tested Models

1. **Grok 4 Fast (free)** - x-ai/grok-4-fast
2. **Grok Code Fast 1** - x-ai/grok-code-fast-1
3. **Claude Sonnet 4.5** - anthropic/claude-sonnet-4.5
4. **Claude Sonnet 4** - anthropic/claude-sonnet-4
5. **Gemini 2.5 Flash** - google/gemini-2.5-flash

## Generated Questions

### 1. Grok Code Fast 1

**Question:** In a tournament where three players—A, B, and C—each compete in a series of one-on-one matches with the following outcomes: A beats B twice, B beats C twice, and A and C tie twice. Unknown is the result of A's match against C. Using only this information, determine the most likely ranking of the players from strongest to weakest, justifying your reasoning step by step. If ties are unavoidable, explain the constraints.

**Generation Time:** 10.31s

### 2. Claude Sonnet 4.5

**Question:** A rectangular swimming pool is being filled by two pipes. Pipe A can fill the pool in 6 hours, and Pipe B can fill it in 4 hours. The pool also has a drain that can empty the full pool in 12 hours.

At 8:00 AM, Pipe A is opened. At 9:00 AM, Pipe B is also opened. At 10:00 AM, someone accidentally opens the drain, which remains open.

However, there's a complication: the pool has a capacity marker at the 75% level. Once the water reaches this marker, a float valve automatically reduces Pipe B's flow rate to half its original rate (Pipe A and the drain are unaffected).

**Questions:**

1. At what time does the water level reach the 75% marker?
2. At what time is the pool completely full?
3. If the pool's total capacity is 2,400 gallons, how many gallons did Pipe B contribute in total?

Show your reasoning for each step, including how you account for the changing rates at different time periods and the flow rate reduction.

**Generation Time:** 14.74s

### 3. Gemini 2.5 Flash

**Question:** A renowned fictional detective, known for solving crimes based on subtle linguistic patterns, is presented with two encrypted messages. Message A, when decrypted, reads: "The quick brown fox jumps over the lazy dog." Message B, when decrypted, reads: "Sphinx of black quartz, judge my vow." The detective is informed that one message was generated by a human, and the other by a sophisticated AI designed to emulate human writing. Without knowing which is which, the detective correctly identifies the AI-generated message.

Based *only* on the decrypted content, and assuming both messages are valid English sentences, what is the *most plausible* linguistic pattern the detective likely used to distinguish the AI-generated message, and why? Justify your reasoning by comparing linguistic features present or absent in each message as they relate to typical human vs. AI text generation.

**Generation Time:** 1.93s

### 4. Claude Sonnet 4

**Question:** A pharmaceutical company discovers that their new drug increases patient recovery rates by 40% in clinical trials, but the trials excluded patients over 65, those with kidney disease, and those taking blood thinners—groups that together represent 60% of the target patient population. The company's marketing team wants to advertise "40% faster recovery" while the medical team argues this is misleading. Meanwhile, a competitor's drug shows only 25% improvement but was tested on the full patient population including all excluded groups.

Analyze the ethical, statistical, and business implications of this scenario. What factors should guide the company's decision about how to market their drug, and how should healthcare providers and patients interpret and compare these competing claims? Consider both the immediate consequences and long-term effects on medical research practices, patient trust, and public health outcomes.

**Generation Time:** 6.43s

### 5. Grok 4 Fast (free)

**Question:** Consider a remote village where villagers are either Truth-tellers (always honest), Liars (always dishonest), or Alternators (who alternate between truth and lies in consecutive statements, starting with truth). You encounter three villagers, X, Y, and Z, each making two statements in order:

- X says: "Y is a Liar" then "Z is an Alternator."
- Y says: "Z is a Truth-teller" then "X is a Liar."
- Z says: "X is an Alternator" then "Y is a Truth-teller."

You also know that exactly one is an Alternator, and no two are the same type. Determine the type of each villager, showing your step-by-step reasoning by considering possible cases for the Alternator and checking consistency with the statements and constraints.

**Generation Time:** 15.03s

## Model Performance Summary

### Overall Average Ratings (10-point scale)

1. **Claude Sonnet 4.5**: 7.58/10
2. **Grok 4 Fast (free)**: 7.44/10
3. **Claude Sonnet 4**: 7.38/10
4. **Grok Code Fast 1**: 6.96/10
5. **Gemini 2.5 Flash**: 6.67/10

### Cross-Model Rating Matrix

This shows how each model (rater/columns) rated each model's answers (answerer/rows):

rater_model_name    Claude Sonnet 4  Claude Sonnet 4.5  Gemini 2.5 Flash  Grok 4 Fast (free)  Grok Code Fast 1
answer_model_name
Claude Sonnet 4                 6.6                6.5               8.4                 6.6               8.6
Claude Sonnet 4.5               7.4                7.0               8.4                 6.4               8.6
Gemini 2.5 Flash                6.8                6.5               8.0                 5.4               6.6
Grok 4 Fast (free)              7.2                6.8               9.4                 7.0               6.8
Grok Code Fast 1                6.0                6.5               7.2                 6.8               8.2

For detailed results and methodology, see the [llm-compare notebook](notebooks/llm-compare.ipynb).

## License

This project is licensed under the MIT License.
