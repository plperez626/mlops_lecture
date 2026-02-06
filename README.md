# MLOps Lecture

# Mini-labs

## Set-up

### Introducing uv as new standard package-manager

```bash
# Install uv package manager
pip install uv

# Install Python 3.11
uv python install 3.11

# Pin Python version to 3.11 for this project
uv python pin 3.11

# Sync dependencies from pyproject.toml
uv sync
```

### useful cmds
```bash
# Run the main script
uv run main.py

# Convert requirements.txt to uv like pyproject.toml
uv add -r requirements.txt
```

