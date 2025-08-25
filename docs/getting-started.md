# Getting Started

## Prerequisites

Before installing Loopy Agents, ensure you have the following:

- Python 3.9 or higher
- Claude Code CLI
- Git
- UV (for single-file agents)

## Installation

### Step 1: Install Claude Code

=== "macOS/Linux"

    ```bash
    # Install via npm
    npm install -g @anthropic/claude-code
    
    # Or use the installer script
    curl -fsSL https://claude.ai/install.sh | sh
    
    # Verify installation
    claude --version
    ```

=== "Windows"

    ```powershell
    # Install via npm
    npm install -g @anthropic/claude-code
    
    # Or download installer from
    # https://claude.ai/download/windows
    
    # Verify installation
    claude --version
    ```

=== "WSL2"

    ```bash
    # In WSL2 terminal
    curl -fsSL https://claude.ai/install.sh | sh
    
    # Add to PATH
    echo 'export PATH="$HOME/.claude/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    
    # Verify installation
    claude --version
    ```

### Step 2: Clone Loopy Agents

```bash
# Clone the repository
git clone https://github.com/looptech-ai/loopy-agents.git
cd loopy-agents

# Install Python dependencies
pip install -r requirements.txt

# Install UV for single-file agents
pip install uv
```

### Step 3: Configure Environment

```bash
# Copy environment template
cp .env.example .env

# Edit with your API keys
nano .env
```

Add your API keys:

```env
# Required
ANTHROPIC_API_KEY=sk-ant-xxxxx

# Optional
OPENAI_API_KEY=sk-xxxxx
GROQ_API_KEY=gsk-xxxxx
ELEVENLABS_API_KEY=xxxxx

# Configuration
MONITORING_PORT=8080
LOG_LEVEL=INFO
```

### Step 4: Initialize Hooks

```bash
# Run the initialization script
python scripts/init_hooks.py

# This will:
# - Create .claude/hooks/ directory
# - Install default hooks
# - Configure settings.json
# - Set up monitoring

# Verify hooks are installed
claude hooks list
```

## Your First Agent

### Create a Simple Agent

Create `my_agent.py`:

```python
#!/usr/bin/env python3
# /// script
# requires-python = ">=3.9"
# dependencies = [
#   "openai",
#   "rich",
# ]
# ///

"""My first Loopy Agent"""

import sys
from rich.console import Console

console = Console()

def main(task: str):
    """Process the task"""
    console.print(f"[green]Processing:[/green] {task}")
    
    # Your agent logic here
    result = f"Completed: {task}"
    
    console.print(f"[cyan]Result:[/cyan] {result}")
    return result

if __name__ == "__main__":
    if len(sys.argv) > 1:
        main(sys.argv[1])
    else:
        console.print("[red]Usage:[/red] python my_agent.py <task>")
```

### Run the Agent

```bash
# Make executable
chmod +x my_agent.py

# Run with UV (auto-installs dependencies)
./my_agent.py "Analyze this code"

# Or run with Python
python my_agent.py "Write a function"
```

## Testing Your Setup

### Test Hooks

```bash
# Test safety hook (should block)
claude "Delete all files with rm -rf /"
# Output: ❌ Blocked by safety hook

# Test normal command (should work)
claude "List files in current directory"
# Output: ✅ Executes normally
```

### Test Monitoring

```bash
# Start monitoring dashboard
python -m loopy_agents.monitor

# Open browser to http://localhost:8080
# You should see the dashboard

# In another terminal, run Claude Code
claude "Create a Python hello world"

# Watch events appear in dashboard
```

### Test MCP Server

```bash
# Start MCP server
python mcp_servers/multi_provider/server.py

# In another terminal
claude --mcp multi-provider "Compare GPT-4 and Claude responses"

# Server will route to appropriate provider
```

## Quick Examples

### Hook Example

```python title=".claude/hooks/user_prompt_submit.py"
#!/usr/bin/env python3
"""Enhance user prompts before submission"""

import json
import sys

def enhance_prompt(event):
    prompt = event.get("prompt", "")
    
    # Add context to coding requests
    if "function" in prompt.lower() or "code" in prompt.lower():
        prompt += "\n\nPlease include: docstrings, type hints, and error handling."
    
    return {
        "action": "continue",
        "prompt": prompt
    }

if __name__ == "__main__":
    event = json.loads(sys.stdin.read())
    result = enhance_prompt(event)
    print(json.dumps(result))
```

### Agent Orchestration

```python title="examples/orchestrate.py"
from loopy_agents import orchestrate

async def review_and_test(file_path):
    """Review code and generate tests"""
    
    tasks = [
        ("code_reviewer", f"Review {file_path}"),
        ("test_writer", f"Write tests for {file_path}"),
        ("documenter", f"Document {file_path}")
    ]
    
    results = await orchestrate(tasks, parallel=True)
    return results

# Run with: python examples/orchestrate.py
```

### Voice Command

```python title="examples/voice.py"
from loopy_agents.voice import listen

# Start listening
command = listen()
print(f"You said: {command}")

# Execute with Claude
from loopy_agents import execute
result = execute(command)
print(f"Result: {result}")
```

## Configuration Files

### `.claude/settings.json`

```json
{
  "hooks": {
    "preToolUse": ".claude/hooks/pre_tool_use.py",
    "postToolUse": ".claude/hooks/post_tool_use.py"
  },
  "mcpServers": {
    "multi-provider": {
      "command": "python",
      "args": ["mcp_servers/multi_provider/server.py"]
    }
  },
  "security": {
    "blockDangerousCommands": true,
    "sandboxExecution": true
  }
}
```

### `CLAUDE.md`

```markdown
# Project Context

## Coding Standards
- Use type hints in Python
- Write comprehensive docstrings
- Include error handling
- Follow PEP 8

## Architecture
- Microservices pattern
- REST APIs
- PostgreSQL database
- Redis caching
```

## Next Steps

Now that you have Loopy Agents installed:

1. **Explore Hooks** - [Learn about lifecycle hooks](hooks/index.md)
2. **Create Agents** - [Build your first agent](agents/single-file.md)
3. **Setup Monitoring** - [Configure observability](observability/index.md)
4. **Connect MCP** - [Add LLM providers](mcp/index.md)

## Troubleshooting

### Common Issues

??? failure "Command 'claude' not found"
    
    Make sure Claude Code is in your PATH:
    
    ```bash
    # Add to ~/.bashrc or ~/.zshrc
    export PATH="$HOME/.claude/bin:$PATH"
    
    # Reload shell
    source ~/.bashrc
    ```

??? failure "ImportError: No module named 'loopy_agents'"
    
    Install the package in development mode:
    
    ```bash
    cd loopy-agents
    pip install -e .
    ```

??? failure "Hook not triggering"
    
    Check your settings file:
    
    ```bash
    # Verify hooks are configured
    cat .claude/settings.json
    
    # Test hook directly
    echo '{"tool_name":"Bash","params":{"command":"ls"}}' | python .claude/hooks/pre_tool_use.py
    ```

??? failure "MCP server timeout"
    
    Increase timeout in settings:
    
    ```json
    {
      "mcpServers": {
        "multi-provider": {
          "timeout": 30000
        }
      }
    }
    ```

## Getting Help

- 📚 [Read the Documentation](https://looptech-ai.github.io/loopy-agents-doc)
- 💬 [Join Discord](https://discord.gg/loopy-agents)
- 🐛 [Report Issues](https://github.com/looptech-ai/loopy-agents/issues)
- 📺 [Watch Tutorials](https://youtube.com/@looptech-ai)