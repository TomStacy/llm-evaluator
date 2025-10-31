# LLM Evaluator

A Python Jupyter Notebook project for evaluating the top Large Language Models (LLMs) according to [OpenRouter](https://openrouter.ai/).

## Credits

[Ed Donner](https://www.udemy.com/user/ed-donner-3/) Udemy Profile

This project is based on an example from Ed Donner in his "Master AI Agents in 30 days: build 8 real-world projects with OpenAI Agents SDK, CrewAI, LangGraph, AutoGen and MCP." course. The orignal code has been modified to use OpenRouter to pull the top 5 most popular LLM's based on OpenRouter Rankings.

## Features

- Python scripts for LLM evaluation
- Jupyter notebooks for interactive analysis
- Modern Python development with uv package manager
- Git version control

## Costs

Running the full question, answer, and evaluate cycle will cost between *$1.50 and $2.50* via OpenRouter.
There are a few past runs captured in the results folder that list both the results and the actual costs pulled directly from the OpenRouter API.

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
├── notebooks/
│   └── llm-compare.ipynb        # LLM comparison notebook
├── .gitignore                   # Git ignore rules
├── .markdownlint.json           # Markdown linting rules
├── .python-version              # Python version specification
├── CODE_REVIEW_SUMMARY.md       # Code review summary
├── pyproject.toml               # Project configuration
├── pyrightconfig.json           # Pyright configuration
├── README.md                    # This file
└── uv.lock                      # Locked dependencies
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

Evaluation Results are located in the results folder

For detailed results and methodology, see the [llm-compare notebook](notebooks/llm-compare.ipynb).

## License

This project is licensed under the MIT License.
