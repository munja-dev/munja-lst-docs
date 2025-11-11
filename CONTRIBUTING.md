# Contributing to Documentation

Thank you for your interest in contributing to the Munja LST documentation!

## Documentation Structure

The documentation is organized using GitBook format:

```
docs/
├── README.md                 # Main landing page
├── SUMMARY.md               # Table of contents (GitBook navigation)
├── book.json                # GitBook configuration
├── .gitbook.yaml            # GitBook settings
├── getting-started/         # Getting started guides
├── contracts/               # Smart contract documentation
├── oracle/                  # Oracle system documentation
├── development/             # Development guides
├── api/                     # API references
├── deployment/              # Deployment guides
└── appendix/                # Glossary, FAQ, troubleshooting
```

## Making Changes

### Prerequisites

1. Fork the repository
2. Clone your fork
3. Create a new branch

```bash
git checkout -b docs/improve-contracts-section
```

### Editing Documentation

1. **Markdown Files**: All documentation is written in Markdown (.md)
2. **GitBook Syntax**: Use standard Markdown with GitBook extensions
3. **Code Blocks**: Use syntax highlighting

```markdown
\`\`\`solidity
function deposit(uint256 amount) external {
// Your code here
}
\`\`\`

\`\`\`rust
fn main() {
println!("Hello, world!");
}
\`\`\`
```

### Adding New Pages

1. Create the markdown file in the appropriate directory
2. Add entry to `SUMMARY.md` in the correct section

```markdown
## Smart Contracts

- [Contracts Overview](contracts/overview.md)
- [New Page Title](contracts/new-page.md) <!-- Add here -->
```

### Local Preview

#### Option 1: GitBook CLI (Recommended)

```bash
# Install GitBook CLI
npm install -g gitbook-cli

# Install plugins
gitbook install

# Serve locally
gitbook serve

# Open http://localhost:4000
```

#### Option 2: Markdown Preview

Use any Markdown previewer:

- VS Code: Built-in preview (Cmd/Ctrl + Shift + V)
- Typora
- Markdown Preview Enhanced (VS Code extension)

## Style Guide

### Headings

Use ATX-style headings:

```markdown
# H1 - Page Title (only one per page)

## H2 - Major Section

### H3 - Subsection

#### H4 - Minor Subsection
```

### Code Examples

Always include:

- Language identifier for syntax highlighting
- Comments explaining complex code
- Complete, runnable examples when possible

```markdown
\`\`\`rust
// Good example with comments
fn verify_proof(proof: &Proof) -> Result<bool> {
// Verify the proof structure
if proof.is_valid() {
Ok(true)
} else {
Err(anyhow!("Invalid proof"))
}
}
\`\`\`
```

### Links

#### Internal Links

Use relative paths:

```markdown
See [Contracts Overview](../contracts/overview.md) for details.
```

#### External Links

Use full URLs:

```markdown
See [SP1 Documentation](https://docs.succinct.xyz) for more information.
```

### Tables

Use GitHub Flavored Markdown tables:

```markdown
| Feature | Description            | Status |
| ------- | ---------------------- | ------ |
| Vaults  | ERC4626 implementation | ✅     |
| Oracle  | ZK verification        | ✅     |
```

### Admonitions

Use blockquotes for notes, warnings, tips:

```markdown
> **Note**: This is an important note.

> **Warning**: Be careful with this operation.

> **Tip**: Pro tip for optimization.
```

### Code References

When referencing code locations, use this format:

```markdown
See `contracts/src/vaults/mMITOc.sol:123` for implementation.
```

## Documentation Sections

### Getting Started

Target audience: New developers

- Prerequisites
- Installation
- Quick start guides
- First-time setup

### Contracts

Target audience: Smart contract developers

- Architecture overview
- Contract details
- Security considerations
- Testing guides

### Oracle

Target audience: Backend/Rust developers

- System architecture
- Service setup
- Configuration
- Deployment

### Development

Target audience: All developers

- Development workflow
- Testing
- Contributing
- Code style

### API Reference

Target audience: Integration developers

- Function signatures
- Parameter descriptions
- Return values
- Examples

## Review Process

1. **Self-Review**: Check for typos, broken links, code accuracy
2. **Build Test**: Ensure GitBook builds without errors
3. **Submit PR**: Create pull request with clear description
4. **Address Feedback**: Respond to review comments
5. **Merge**: Maintainer will merge when approved

## Common Issues

### Broken Links

Check all links before submitting:

```bash
# Install markdown-link-check
npm install -g markdown-link-check

# Check all markdown files
find docs -name "*.md" -exec markdown-link-check {} \;
```

### SUMMARY.md Sync

Ensure all pages are listed in `SUMMARY.md`:

```bash
# Find markdown files not in SUMMARY
grep -r "\.md" docs/ --include="*.md" | \
  grep -v SUMMARY.md | \
  while read line; do
    file=$(echo $line | cut -d: -f1)
    if ! grep -q "$(basename $file)" docs/SUMMARY.md; then
      echo "Missing in SUMMARY.md: $file"
    fi
  done
```

## GitBook Features

### Variables

Use book.json variables:

```markdown
Version: {{ book.version }}
Project: {{ book.project }}
```

### Plugins

Enabled plugins (see book.json):

- `code` - Enhanced code blocks
- `collapsible-menu` - Collapsible navigation
- `github` - GitHub integration
- `anchors` - Heading anchors
- `search-plus` - Advanced search
- `copy-code-button` - Copy button for code blocks
- `prism` - Syntax highlighting

### Math Equations

Use KaTeX for math:

```markdown
Inline: $E = mc^2$

Block:

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
```

## Publishing

Documentation is automatically published when merged to main branch:

1. PR merged to `main`
2. GitHub Actions builds GitBook
3. Deployed to documentation site
4. Available at https://docs.munja.io

## Questions?

- Check existing documentation
- Ask in Discord/Telegram
- Create a GitHub issue
- Contact maintainers

## Thank You!

Your contributions help make Munja LST better for everyone! 🎉
