# 📚 Loopy Agents Documentation

> **Beautiful dark-themed MkDocs Material documentation for the Loopy Agents Claude Code framework**

[![MkDocs](https://img.shields.io/badge/MkDocs-Material-purple?style=for-the-badge)](https://squidfunk.github.io/mkdocs-material/)
[![Deploy](https://img.shields.io/badge/Deploy-GitHub%20Pages-blue?style=for-the-badge)](https://looptech-ai.github.io/loopy-agents-doc)

## 🌐 Live Documentation

Visit: [https://looptech-ai.github.io/loopy-agents-doc](https://looptech-ai.github.io/loopy-agents-doc)

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- pip

### Local Development

```bash
# Clone repository
git clone https://github.com/looptech-ai/loopy-agents-doc.git
cd loopy-agents-doc

# Install dependencies
pip install -r requirements.txt

# Start development server
mkdocs serve

# Visit http://localhost:8000
```

### Using npm scripts

```bash
# Install Python dependencies
npm run install-deps

# Start dev server with live reload
npm run dev

# Build static site
npm run build

# Deploy to GitHub Pages
npm run deploy
```

## 🎨 Features

### Dark Theme by Default
- Beautiful slate color scheme
- Deep purple primary, cyan accent
- Smooth theme toggle
- Optimized for code readability

### Copyable Code Blocks
All code blocks feature:
- ✨ Syntax highlighting
- 📋 One-click copy button
- 🏷️ Language labels
- 📝 Line numbers
- 🎯 Annotations support

### Interactive Elements
- 📑 Tabbed content
- 💡 Admonitions (tips, warnings, etc.)
- 🔍 Instant search
- 📊 Mermaid diagrams
- ✅ Task lists

### Developer Experience
- 🔄 Live reload
- 🚀 Instant navigation
- 📱 Mobile responsive
- ⌨️ Keyboard shortcuts
- 🔗 Deep linking

## 📁 Documentation Structure

```
docs/
├── index.md                 # Homepage
├── getting-started.md       # Quick start guide
├── architecture.md          # System overview
├── hooks/                   # Hook documentation
│   ├── index.md
│   ├── lifecycle.md
│   ├── security.md
│   └── examples.md
├── agents/                  # Agent patterns
│   ├── single-file.md
│   ├── multi-agent.md
│   └── voice-enabled.md
├── mcp/                     # MCP servers
│   ├── nano-agent.md
│   ├── just-prompt.md
│   └── custom-servers.md
├── observability/           # Monitoring
│   ├── monitoring.md
│   ├── real-time.md
│   └── debugging.md
└── examples/                # Code examples
    ├── quick-start.md
    └── advanced.md
```

## 🛠️ Configuration

### Theme Customization
Edit `mkdocs.yml` to customize:
- Colors and fonts
- Navigation structure
- Features and plugins
- Social links

### Custom CSS
Add styles to `docs/stylesheets/extra.css`:
- Gradient animations
- Enhanced code blocks
- Custom components

## 📦 Build & Deploy

### Build Static Site
```bash
mkdocs build
# Output in site/ directory
```

### Deploy to GitHub Pages
```bash
mkdocs gh-deploy --force
```

### CI/CD with GitHub Actions
```yaml
name: Deploy Docs
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.11'
      - run: pip install -r requirements.txt
      - run: mkdocs gh-deploy --force
```

## 🎯 Key Features

### Material Design
- Clean, modern interface
- Responsive layout
- Touch-friendly navigation
- Smooth animations

### Search
- Instant search results
- Fuzzy matching
- Search suggestions
- Keyboard navigation

### Code Blocks
```python
# Example with all features
def example_function(param: str) -> dict:
    """Copyable code with syntax highlighting"""
    return {"result": param}
```

### Tabbed Content
=== "Python"
    ```python
    print("Hello, World!")
    ```

=== "JavaScript"
    ```javascript
    console.log("Hello, World!");
    ```

### Admonitions
!!! tip "Pro Tip"
    Use admonitions for important information

!!! warning "Security"
    Always validate user input

## 🔧 Advanced Configuration

### Plugins
- **search**: Full-text search
- **minify**: HTML/CSS/JS minification  
- **git-revision-date**: Show last updated
- **tags**: Tag-based navigation

### Extensions
- **pymdownx.superfences**: Mermaid diagrams
- **pymdownx.tabbed**: Tabbed content
- **pymdownx.tasklist**: Checkboxes
- **pymdownx.highlight**: Advanced syntax

## 📈 Analytics

Configure Google Analytics in `mkdocs.yml`:
```yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make your changes
4. Test locally with `mkdocs serve`
5. Submit pull request

## 📝 Writing Documentation

### Best Practices
- Use clear, concise language
- Include code examples
- Add screenshots where helpful
- Test all code snippets
- Keep navigation logical

### Markdown Features
- Headers with anchors
- Tables with sorting
- Footnotes
- Abbreviations
- Definition lists

## 🐛 Troubleshooting

### Common Issues

**Build fails:**
```bash
# Clear cache
rm -rf site/
mkdocs build --clean
```

**Dependencies error:**
```bash
# Upgrade pip and reinstall
pip install --upgrade pip
pip install -r requirements.txt --force-reinstall
```

**GitHub Pages 404:**
```bash
# Ensure gh-pages branch exists
mkdocs gh-deploy --force
```

## 📚 Resources

- [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
- [MkDocs Documentation](https://www.mkdocs.org/)
- [Markdown Guide](https://www.markdownguide.org/)
- [Mermaid Diagrams](https://mermaid.js.org/)

## 📄 License

MIT License - See [LICENSE](LICENSE) file

## 🙏 Credits

- Built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)
- Based on research from disler/IndyDevDan
- Inspired by Claude Code community

---

<div align="center">

**Ready to build beautiful documentation?**

[View Live Docs](https://looptech-ai.github.io/loopy-agents-doc) | [Main Repository](https://github.com/looptech-ai/loopy-agents)

</div>