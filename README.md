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

2. Install dependencies using uv:
```bash
uv sync
```

This will create a virtual environment and install all required packages including Jupyter.

## Project Structure

```
llm-evaluator/
├── .github/
│   └── copilot-instructions.md  # Copilot configuration
├── notebooks/                    # Jupyter notebooks
│   └── example.ipynb            # Example notebook
├── src/                         # Source code
│   └── llm_evaluator/          # Main package
│       └── __init__.py
├── tests/                       # Test files
├── .gitignore                   # Git ignore rules
├── pyproject.toml              # Project configuration
├── README.md                   # This file
└── uv.lock                     # Locked dependencies
```

## Usage

### Running Python Scripts

```bash
uv run python src/llm_evaluator/__init__.py
```

### Using Jupyter Notebooks

1. Start Jupyter:
```bash
uv run jupyter notebook
```

2. Navigate to the `notebooks/` directory and open any `.ipynb` file.

Alternatively, open notebooks directly in VS Code with the Jupyter extension.

### Running Tests

```bash
uv run pytest tests/
```

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
2. Make your changes
3. Run tests to ensure everything works
4. Submit a pull request

## License

This project is licensed under the MIT License.
