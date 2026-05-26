# playground-ai

Personal AI learning playground for Python, Jupyter notebooks, API experiments, and notes.

This repo is intended to be a safe place to experiment while avoiding accidental commits of virtual environments, API keys, `.env` files, generated outputs, or other sensitive local files.

## What this repo includes

- `.gitignore` — excludes `.venv`, `.env`, notebook checkpoints, caches, build artifacts, logs, and local output folders.
- `.env.example` — template for API keys and secrets.
- `requirements.txt` — starter Python packages for notebooks and AI API work.
- `README.md` — cross-platform setup guide for Windows, macOS, and Linux.

## Recommended VS Code extensions

Install these from the VS Code Extensions panel:

- **Python** by Microsoft
- **Jupyter** by Microsoft
- **Pylance** by Microsoft
- **Ruff** by Astral Software
- **GitLens** by GitKraken, optional but useful
- **GitHub Pull Requests** by GitHub, optional
- **dotenv** extension, optional for `.env` syntax highlighting

You can also install the core extensions from the terminal after VS Code is installed:

```bash
code --install-extension ms-python.python
code --install-extension ms-toolsai.jupyter
code --install-extension ms-python.vscode-pylance
code --install-extension charliermarsh.ruff
```

## Install Python

Use Python 3.11 or newer.

### Windows

Recommended: install Python from <https://www.python.org/downloads/windows/>.

During installation, check:

```text
Add python.exe to PATH
```

Confirm installation in PowerShell:

```powershell
python --version
python -m pip --version
```

If `python` does not work, try the Windows Python launcher:

```powershell
py --version
py -m pip --version
```

### macOS

Option 1, using Homebrew:

```zsh
brew install python
python3 --version
python3 -m pip --version
```

Option 2: install Python from <https://www.python.org/downloads/macos/>.

### Linux

Debian / Ubuntu:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
python3 --version
python3 -m pip --version
```

Fedora:

```bash
sudo dnf install python3 python3-pip
python3 --version
python3 -m pip --version
```

Arch Linux:

```bash
sudo pacman -S python python-pip
python --version
python -m pip --version
```

## Create the project folder

### Windows PowerShell

```powershell
mkdir playground-ai
cd playground-ai
git init
```

### macOS / Linux

```bash
mkdir playground-ai
cd playground-ai
git init
```

Copy the files from this starter repo into the folder.

## Create a virtual environment

### Windows PowerShell

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

If PowerShell blocks activation, run this once:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Then activate again:

```powershell
.\.venv\Scripts\Activate.ps1
```

### Windows Command Prompt

```bat
python -m venv .venv
.venv\Scripts\activate.bat
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On some Linux distributions, the command may be `python` instead of `python3`:

```bash
python -m venv .venv
source .venv/bin/activate
```

## Deactivate the virtual environment

This works on Windows, macOS, and Linux:

```bash
deactivate
```

## Register the Jupyter kernel

After activating `.venv`, run this on any platform:

```bash
python -m ipykernel install --user --name playground-ai --display-name "Python (.venv playground-ai)"
```

This makes your virtual environment show up as a selectable notebook kernel.

## Use notebooks in VS Code

1. Open the `playground-ai` folder in VS Code.
2. Open the Command Palette:
   - Windows/Linux: `Ctrl+Shift+P`
   - macOS: `Cmd+Shift+P`
3. Run **Python: Select Interpreter**.
4. Choose the interpreter inside `.venv`:
   - Windows: `.venv\Scripts\python.exe`
   - macOS/Linux: `.venv/bin/python`
5. Create or open a `.ipynb` notebook.
6. In the top-right notebook kernel picker, select:

```text
Python (.venv playground-ai)
```

## Working with `.env` files safely

Create your real local `.env` file from the example.

### Windows PowerShell

```powershell
Copy-Item .env.example .env
```

### Windows Command Prompt

```bat
copy .env.example .env
```

### macOS / Linux

```bash
cp .env.example .env
```

Add your real API keys to `.env`. The `.gitignore` prevents `.env` from being committed.

Example Python usage:

```python
from dotenv import load_dotenv
import os

load_dotenv()

openai_api_key = os.getenv("OPENAI_API_KEY")
```

## First notebook test

Create a folder named `notebooks`, then create a notebook named `hello.ipynb`.

### Windows PowerShell

```powershell
mkdir notebooks
```

### macOS / Linux

```bash
mkdir -p notebooks
```

In `notebooks/hello.ipynb`, select the `playground-ai` kernel and run:

```python
import sys
print(sys.executable)
```

You should see a path pointing to your project’s `.venv` folder.

Then test packages:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

pd.DataFrame({"status": ["ready"], "project": ["playground-ai"]})
```

## Git safety check before committing

Before your first commit, run this on any platform:

```bash
git status
```

Make sure these are **not** listed as files to commit:

- `.venv/`
- `.env`
- API keys
- large generated data/model/output files

Then commit:

```bash
git add .
git commit -m "Initial playground-ai setup"
```

## Optional: using uv instead of pip

The `llm_engineering` course repo has moved toward `uv` for faster Python environment management. `uv` can be a good option later, but plain `venv` + `pip` is simpler while learning.

Install `uv` after activating your virtual environment:

```bash
python -m pip install uv
```

Then, in the project folder:

```bash
uv venv
uv pip install -r requirements.txt
```

For now, either workflow is fine. Do not mix tools unless you know why you are switching.

## Suggested folder structure

```text
playground-ai/
├── .env.example
├── .gitignore
├── README.md
├── requirements.txt
├── notebooks/
│   └── hello.ipynb
├── src/
│   └── playground_ai/
└── notes/
```

## Common fixes

### The notebook cannot find installed packages

You are probably using the wrong kernel. Select the `.venv` / `playground-ai` kernel in the notebook picker.

### `pip` is missing

Try this after activating the virtual environment:

```bash
python -m ensurepip --upgrade
python -m pip install --upgrade pip
```

### `python` works on Windows but not macOS/Linux

Use `python3` on macOS/Linux:

```bash
python3 --version
python3 -m pip --version
```

### `python3` works on Linux/macOS but not Windows

Use `python` or `py` on Windows:

```powershell
python --version
py --version
```
