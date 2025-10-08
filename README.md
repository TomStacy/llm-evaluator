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

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd llm-evaluator
   ```

1. Install dependencies using uv:

   ```bash
   uv sync
   ```

   This will create a virtual environment and install all required packages including Jupyter.

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

### Using Jupyter Notebooks

1. Start Jupyter:

   ```bash
   uv run jupyter notebook
   ```

1. Navigate to the `notebooks/` directory and open any `.ipynb` file.

Alternatively, open notebooks directly in VS Code with the Jupyter extension.

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

#### Generated Questions

##### 1. Grok Code Fast 1

**Question:** In a hypothetical society, all inhabitants are either Knights who always tell the truth or Knaves who always lie. You encounter three people: A, B, and C. A says, "We are all Knaves." B says, "Exactly one of us is a Knight." C says, "B and I are different types." Determine the type of each person (Knight or Knave) and provide a step-by-step explanation of your reasoning.

**Generation Time:** 5.6s

##### 2. Claude Sonnet 4.5

**Question:** A rectangular swimming pool is being filled by two pipes. Pipe A fills at a constant rate, while Pipe B's flow rate decreases by 10% each hour. When both pipes run together from the start, the pool fills in exactly 6 hours. When only Pipe A runs, it takes 10 hours to fill the pool. If the pool is empty and you run only Pipe B for 3 hours, then turn it off and finish filling the pool with only Pipe A, how long will the entire process take?

**Generation Time:** 5.26s

##### 3. Gemini 2.5 Flash

**Question:** You are presented with a series of nested, opaque containers. Container A contains either Container B or Container C, but not both. Container B contains either a red marble or a blue marble, and also either Container D or Container E. If you are told that you have successfully identified a red marble, and you know definitively that you did *not* open Container C, what is the *single most probable sequence of containers* you opened?

**Generation Time:** 1.63s

##### 4. Grok 4 Fast (free)

**Question:** Suppose you have a rectangular garden that measures 12 meters by 8 meters, and you want to divide it into smaller square plots of equal size, using as few plots as possible without leaving any unused land. What is the side length of each square plot, and how many such plots are there? If the garden were instead 12 meters by 9 meters, explain how the number of plots would change and why.

**Generation Time:** 9.74s

##### 5. Claude Sonnet 4

**Question:** A rectangular garden has a perimeter of 100 meters. Inside this garden, there are two circular flower beds that do not overlap, each with a radius of 8 meters. If you want to place a square gazebo somewhere in the remaining space such that it doesn't overlap with either flower bed, what is the maximum possible side length of this square gazebo?

**Generation Time:** 3.54s

#### Model Performance Summary

##### Overall Average Ratings (10-point scale)

1. 🥇 **Grok 4 Fast (free)**: 8.67/10
2. 🥈 **Grok Code Fast 1**: 7.21/10
3. 🥉 **Claude Sonnet 4.5**: 6.92/10
4. **Claude Sonnet 4**: 6.40/10
5. **Gemini 2.5 Flash**: 6.38/10

#### Cross-Model Rating Matrix

This matrix shows how each model (columns) rated each model's answers (rows):

| Answer Model | Claude Sonnet 4 | Claude Sonnet 4.5 | Gemini 2.5 Flash | Grok 4 Fast | Grok Code Fast 1 |
|--------------|-----------------|-------------------|------------------|-------------|------------------|
| **Claude Sonnet 4** | 6.40 | 6.60 | 6.80 | 5.60 | 6.60 |
| **Claude Sonnet 4.5** | 7.00 | 6.80 | 8.00 | 6.40 | 6.40 |
| **Gemini 2.5 Flash** | 6.60 | 6.75 | 7.20 | 5.40 | 6.00 |
| **Grok 4 Fast (free)** | 8.67 | 7.67 | 9.33 | 8.00 | 9.67 |
| **Grok Code Fast 1** | 6.80 | 6.00 | 6.60 | 8.40 | 8.00 |

#### Key Findings

- **Grok 4 Fast (free)** achieved the highest overall rating (8.67/10), consistently receiving strong scores across all raters
- **Grok Code Fast 1** came in second (7.21/10), showing particularly strong performance when rated by Grok 4 Fast (9.67/10)
- The Claude models and Gemini 2.5 Flash performed similarly, with scores between 6.38-6.92
- There is notable variance in how different models rate the same answers, suggesting subjective differences in evaluation criteria
- Generation times varied from 1.63s (Gemini 2.5 Flash) to 9.74s (Grok 4 Fast)

For detailed results and methodology, see the [llm-compare notebook](notebooks/llm-compare.ipynb).

## License

This project is licensed under the MIT License.
