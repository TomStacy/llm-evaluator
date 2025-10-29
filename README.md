# LLM Evaluator

A Python project for evaluating Large Language Models (LLMs) using the uv package manager.

## Credits

[Ed Donner](https://www.udemy.com/user/ed-donner-3/) Udemy Profile

This project is based on an example from Ed Donner in his "Master AI Agents in 30 days: build 8 real-world projects with OpenAI Agents SDK, CrewAI, LangGraph, AutoGen and MCP." course. The orignal code has been modified to use OpenRouter to pull the top 5 most popular LLM's based on OpenRouter Rankings.

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

#### Tested Models (10/28/2025)

| Model | Score |
|-------|-------|
| Grok Code Fast 1 | 1.35T tokens (16% change) |
| Claude Sonnet 4.5 | 569.0B tokens (5% change) |
| Gemini 2.5 Flash | 298.0B tokens (0% change) |
| Gemini 2.5 Pro | 184.0B tokens (18% change) |
| Grok 4 Fast | 160.0B tokens (15% change) |

## Generated Questions

### 1. Grok Code Fast 1

**Question:** A hiker is lost in the woods and knows that a town lies precisely due east. She has a faulty compass that points north only 80% of the time, but otherwise points randomly in any direction. She can take only one step before rechecking the compass. Assuming the woods are uniform and she has no other tools, describe a strategy for her to maximize the probability of heading towards the town, including the reasoning for why this approach is optimal, any assumptions made, and how partial failures are mitigated. Explain step-by-step.

**Generation Time:** 9.51s

### 2. Claude Sonnet 4.5

**Question:** ## The Lighthouse Problem

A lighthouse keeper notices that her lighthouse beam rotates at a constant rate of one complete rotation every 60 seconds. The lighthouse sits on a small island 2 kilometers from a perfectly straight shoreline.

**Part A:** At the moment when the beam is perpendicular to the shore, it illuminates a point P on the beach. How fast is this illuminated point P traveling along the shoreline at that exact instant?

**Part B:** When the beam makes a 60-degree angle with the perpendicular to the shore, how fast is the illuminated point traveling along the shoreline at that moment?

**Part C:** The keeper decides to install a motion sensor that will trigger whenever the illuminated point on the shore is traveling faster than 1 kilometer per second. What is the total length of shoreline (combining sections on both sides of the perpendicular) where this sensor would need to be installed?

**Part D:** A sailor in a boat parallel to the shore argues that if the beam rotates fast enough, the illuminated point could theoretically exceed the speed of light. The keeper dismisses this as impossible. Who is correct and why? If the sailor is correct, at what angle(s) from the perpendicular would the illuminated point first exceed the speed of light if the rotation rate were increased to 10 rotations per second?

Show your reasoning for each part, including the mathematical relationships you use and any assumptions you make.

**Generation Time:** 8.93s

### 3. Gemini 2.5 Flash

**Question:** A cryptographer designs a system where a message, M, is encrypted by applying two operations: first, a bitwise XOR with a 64-bit key, K, then a cyclic left shift by a variable amount, S. Decryption reverses this: a cyclic right shift by S, then a bitwise XOR with K.

An attacker intercepts two encrypted messages, C1 and C2, and knows they both originated from the same plaintext P, but were encrypted using different (unknown) shift amounts, S1 and S2 (where S1 != S2). The key K is the same for both.

Given only C1, C2, and the knowledge that K contains at least two consecutive '1' bits and at least two consecutive '0' bits, deduce a strategy to recover K without knowing S1, S2, or P. Explain the crucial property of XOR and cyclic shifts that makes this feasible, and outline the steps you would take, acknowledging any potential ambiguities or remaining unknowns about K.

**Generation Time:** 1.94s

### 4. Gemini 2.5 Pro

**Question:** Consider a closed system with three logic-driven Constructs: Alpha, Beta, and Gamma, arranged in a fixed processing loop (Alpha sends to Beta, Beta to Gamma, Gamma to Alpha). You can trigger one Construct per turn. When triggered, a Construct processes the last signal it received and sends a new one.

The system has these rules:

1. **Transformation:**

    - If a Construct receives a Pulse, its next signal will be a Wave.
    - If a Construct receives a Wave, its next signal will be a Chord.
    - If a Construct receives a Chord, it enters a "Resonant State" and its next signal will replicate the *second-to-last* signal it received. If no second-to-last signal exists, it sends a Pulse.
2. **Harmonic Interference:** If, at the start of a turn, both Alpha and Gamma hold a Wave as their "next signal to be sent," Beta becomes "desynchronized." A desynchronized Construct cannot be triggered and will not send or receive a signal for that turn. It automatically resynchronizes at the end of the turn.

**Initial State (Turn 0):**

- The last signal Alpha received was a Pulse.
- The last signal Beta received was a Wave.
- The last signal Gamma received was a Wave.

Your task is to determine the shortest sequence of triggers to make Beta send a Pulse.

For each turn in your sequence, specify:
a) Which Construct you trigger.
b) The resulting signal sent by the triggered Construct.
c) The state of all three Constructs for the next turn (i.e., what is the last signal each has now received?).
d) A brief justification, explaining how your choice navigates the rules to achieve the goal.

**Generation Time:** 26.36s

### 5. Grok 4 Fast

**Question:** Suppose you are designing a secure messaging app where messages are encrypted using a shared key derived from a sequence of operations on user inputs. The key generation starts with two prime numbers, p=17 and q=23, and a user's passphrase hashed to an integer m=42. The process is: (1) Compute the product n = p * q. (2) Compute Euler's totient φ(n). (3) Select e=5 (coprime to φ(n)). (4) Compute d such that d * e ≡ 1 mod φ(n). Now, to send a message x (where 0 < x < n), compute ciphertext c = x^e mod n using d for decryption. However, to add nuance for security, the app modifies step 4: instead of modular inverse, it uses d = (φ(n) + 1) / e if integer, else falls back to the inverse. For m=42, adjust e to the smallest odd integer greater than 1 coprime to φ(n) if 5 isn't used.

a) Compute n, φ(n), and the adjusted e if needed.  
b) Compute d using the modified rule.  
c) If the message x=15, what is c? Verify decryption recovers x.  
d) Explain why this modification might weaken or strengthen the security, considering RSA principles.

**Generation Time:** 6.92s

## Model Performance Summary

### Overall Average Ratings (10-point scale)

1. **Gemini 2.5 Pro**: 9.60/10
2. **Grok 4 Fast**: 9.12/10
3. **Claude Sonnet 4.5**: 8.04/10
4. **Gemini 2.5 Flash**: 7.92/10
5. **Grok Code Fast 1**: 7.56/10

### Cross-Model Rating Matrix

This shows how each model (rater/columns) rated each model's answers (answerer/rows):

| Model | Claude Sonnet 4.5 | Gemini 2.5 Flash | Gemini 2.5 Pro | Grok 4 Fast | Grok Code Fast 1 |
| --- | --- | --- | --- | --- | --- |
| Claude Sonnet 4.5 | 6.40 | 7.80 | 10.00 | 7.80 | 8.20 |
| Gemini 2.5 Flash | 6.40 | 9.40 | 8.00 | 7.20 | 8.60 |
| Gemini 2.5 Pro | 8.20 | 10.00 | 10.00 | 9.80 | 10.00 |
| Grok 4 Fast | 6.40 | 9.40 | 10.00 | 9.80 | 10.00 |
| Grok Code Fast 1 | 7.00 | 8.60 | 6.40 | 7.40 | 8.40 |

## Rating Statistics Summary

### 📊 Overall Rating Distribution

- **Total ratings collected**: 125
- **Average rating**: 8.45 / 10
- **Median rating**: 10.0 / 10
- **Standard deviation**: 2.50
- **Range**: 1 - 10

### 📈 Rating Frequency

- **10/10**: `███████████` (71 ratings, 56.8%)
- **9/10**: `█` (12 ratings, 9.6%)
- **8/10**: `██` (13 ratings, 10.4%)
- **7/10**: `█` (12 ratings, 9.6%)
- **6/10**: `` (3 ratings, 2.4%)
- **5/10**: `` (1 ratings, 0.8%)
- **4/10**: `` (2 ratings, 1.6%)
- **3/10**: `` (3 ratings, 2.4%)
- **2/10**: `` (2 ratings, 1.6%)
- **1/10**: `` (6 ratings, 4.8%)

### 🤔 Self-Rating vs. Peer-Rating

- **Average when rating own answers**: 8.80
- **Average when rating others' answers**: 8.36
- **Bias Analysis**: Models are fairly unbiased (difference: +0.44)

### 🎭 Rater Characteristics

- **🎁 Most Generous Rater**: Gemini 2.5 Flash (avg: 9.04)
- **🔍 Strictest Rater**: Claude Sonnet 4.5 (avg: 6.88)
- **📏 Rater Spread**: 2.16 points

For detailed results and methodology, see the [llm-compare notebook](notebooks/llm-compare.ipynb).

## License

This project is licensed under the MIT License.
