# Claude Code Configuration

This directory contains all Claude Code configuration for the Playwright + TypeScript UI test automation template.

## 📁 Structure

```
.claude/
├── commands/              # Slash commands for interactive workflows
│   ├── review-tests.md
│   ├── add-smoke-test.md
│   ├── add-regression-test.md
│   ├── create-pom.md
│   ├── run-tests.md
│   ├── analyze-coverage.md
│   ├── setup-ci.md
│   ├── debug-test.md
│   └── generate-test-data.md
│
├── agents/                # Autonomous agent configurations
│   ├── test-writer.md     # Agent for writing professional tests
│   └── code-reviewer.md   # Agent for code review and quality checks
│
├── PROJECT_PLAN.md        # Complete project plan and roadmap
├── MCP_RECOMMENDATIONS.md # MCP server setup and usage guide
├── SETUP_GUIDE.md         # Setup instructions for Claude Code
├── AGENTS_GUIDE.md        # Guide for using autonomous agents
└── README.md              # This file
```

## 🎯 Quick Links

### Essential Documentation
- **[SETUP_GUIDE.md](SETUP_GUIDE.md)** - Start here! Complete setup instructions
- **[PROJECT_PLAN.md](PROJECT_PLAN.md)** - Comprehensive project roadmap
- **[AGENTS_GUIDE.md](AGENTS_GUIDE.md)** - How to use autonomous agents

### Configuration Files
- **[commands/](commands/)** - 9 interactive slash commands
- **[agents/](agents/)** - 2 autonomous agents

### Additional Resources
- **[MCP_RECOMMENDATIONS.md](MCP_RECOMMENDATIONS.md)** - MCP server setup guide

## 🚀 Quick Start

### 1. Interactive Workflows (Slash Commands)

Use slash commands for guided, interactive task completion:

```bash
# Review test code
/review-tests tests/smoke/homepage.spec.ts

# Create new tests
/add-smoke-test
/add-regression-test

# Create Page Objects
/create-pom HomePage

# Run tests
/run-tests

# Analyze coverage
/analyze-coverage

# Debug tests
/debug-test tests/smoke/homepage.spec.ts

# Generate test data
/generate-test-data

# Setup CI/CD
/setup-ci
```

### 2. Autonomous Agents

Use agents for complex, multi-step tasks that run autonomously:

```bash
# Write tests (researches page, creates POMs, writes tests)
Launch test-writer agent to create smoke tests for product search

# Review code (checks quality, runs tests, provides verdict)
Launch code-reviewer agent to review the search tests
```

## 📊 When to Use What?

### Use Slash Commands For:
- ✅ Interactive, guided workflows
- ✅ Learning and exploration
- ✅ Quick tasks with human input
- ✅ Step-by-step guidance

### Use Agents For:
- ✅ Complex, multi-step tasks
- ✅ Autonomous work (minimal interaction)
- ✅ Complete feature implementation
- ✅ Code review and quality checks

## 🎓 Available Slash Commands

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/review-tests` | Review test code quality | Before pushing code |
| `/add-smoke-test` | Create smoke test | Adding critical path tests |
| `/add-regression-test` | Create regression test | Adding comprehensive tests |
| `/create-pom` | Create Page Object Model | Modeling new pages |
| `/run-tests` | Execute tests | Running specific test suites |
| `/analyze-coverage` | Analyze test coverage | Identifying gaps |
| `/setup-ci` | Setup CI/CD | Configuring automation |
| `/debug-test` | Debug failing test | Troubleshooting failures |
| `/generate-test-data` | Generate test fixtures | Creating test data |

## 🤖 Available Agents

| Agent | Purpose | When to Use |
|-------|---------|-------------|
| `test-writer` | Write professional tests autonomously | Creating new test suites |
| `code-reviewer` | Review code and provide verdict | Before git push |

## 📋 Recommended Workflows

### Workflow 1: Creating New Tests (Interactive)

```
1. /analyze-coverage
   → Identify what needs testing

2. /create-pom ProductPage
   → Create necessary Page Objects

3. /add-smoke-test
   → Create the test (guided)

4. /review-tests tests/smoke/product.spec.ts
   → Review code quality

5. /run-tests
   → Execute and verify
```

### Workflow 2: Creating New Tests (Autonomous)

```
1. Launch test-writer agent
   "Create regression tests for checkout flow"
   → Agent researches, creates POMs, writes tests

2. Launch code-reviewer agent
   "Review checkout tests"
   → Agent reviews, runs tests, provides verdict

3. Follow recommendation
   → Push to git or refine based on verdict
```

### Workflow 3: Code Review Before Push

```
1. /review-tests tests/regression/
   → Quick code review

2. Launch code-reviewer agent
   "Review all recent test changes"
   → Comprehensive review with verdict

3. Follow recommendation
   → Push or fix issues
```

## 🔧 Configuration Details

### Slash Commands
- **Location**: `.claude/commands/*.md`
- **Format**: Markdown with frontmatter
- **Invocation**: Type `/` in Claude Code
- **Customization**: Edit `.md` files

### Agents
- **Location**: `.claude/agents/*.md`
- **Format**: Markdown with frontmatter
- **Invocation**: `Launch [agent-name] agent`
- **Customization**: Edit agent configuration files

### MCP Servers
- **Recommended**: Microsoft Playwright MCP
- **Setup**: See [MCP_RECOMMENDATIONS.md](MCP_RECOMMENDATIONS.md)
- **Usage**: Enhanced page exploration and research

## 📚 Documentation

### Getting Started
1. Read [SETUP_GUIDE.md](SETUP_GUIDE.md) for initial setup
2. Review [PROJECT_PLAN.md](PROJECT_PLAN.md) for project structure
3. Try slash commands for interactive work
4. Experiment with agents for autonomous tasks

### Advanced Usage
- [AGENTS_GUIDE.md](AGENTS_GUIDE.md) - Detailed agent usage
- [MCP_RECOMMENDATIONS.md](MCP_RECOMMENDATIONS.md) - MCP integration
- [commands/](commands/) - Individual command documentation

## 🎯 Best Practices

### Using Slash Commands
✅ Use for learning and exploration
✅ Review generated code
✅ Customize commands for your needs
❌ Don't blindly accept all code
❌ Don't skip testing

### Using Agents
✅ Provide clear requirements
✅ Let agents work autonomously
✅ Always review agent output
✅ Follow agent recommendations
❌ Don't micromanage agents
❌ Don't skip code review step

## 🔄 Workflow Recommendations

### Daily Development
```
Morning:
- /analyze-coverage → Plan the day

During Development:
- test-writer agent → Create tests
- /create-pom → Build Page Objects

Before Commit:
- code-reviewer agent → Review quality
- /run-tests → Verify functionality

Before Push:
- code-reviewer agent → Final check
- Follow verdict
```

### Code Review Day
```
1. Launch code-reviewer agent
   "Review all tests in tests/smoke/"

2. Address issues found

3. Re-review if needed

4. Push when approved
```

## 💡 Tips & Tricks

### Combining Tools
```bash
# Use MCP for research, then slash command for creation
1. "Navigate to the target page and analyze structure" (MCP)
2. /create-pom PageName (Slash command)
3. /add-regression-test (Slash command)

# Or use agent for complete automation
Launch test-writer agent to create tests for specific feature
```

### Efficient Workflows
```bash
# For learning: Use slash commands (interactive)
# For productivity: Use agents (autonomous)
# For quality: Always use code-reviewer before push
```

## 🐛 Troubleshooting

### Slash Commands Not Working
- Check `.claude/commands/` exists
- Verify `.md` file format
- Restart Claude Code

### Agents Not Responding
- Check `.claude/agents/` exists
- Verify agent file format
- Simplify request

### MCP Issues
```bash
# Check installation
claude mcp list

# Reinstall if needed
claude mcp add microsoft/playwright-mcp
```

## 📈 Success Metrics

You're using Claude Code effectively when:
- ✅ Commands and agents work smoothly
- ✅ Code quality is consistently high
- ✅ Test coverage is comprehensive
- ✅ Workflow is efficient
- ✅ Code reviews catch issues early
- ✅ Tests pass reliably

## 🎓 Learning Path

### Week 1: Learn Commands
- Try each slash command
- Understand their purpose
- Customize if needed

### Week 2: Learn Agents
- Experiment with test-writer
- Use code-reviewer
- Understand the workflow

### Week 3: Optimize Workflow
- Combine commands and agents
- Find your preferred workflow
- Improve efficiency

### Week 4: Master the System
- Create custom commands
- Modify agent behavior
- Share best practices

## 🚀 Next Steps

1. **Read the setup guide:**
   ```bash
   cat SETUP_GUIDE.md
   ```

2. **Try a slash command:**
   ```
   /review-tests
   ```

3. **Launch an agent:**
   ```
   Launch test-writer agent to create a simple test
   ```

4. **Review the project plan:**
   ```bash
   cat PROJECT_PLAN.md
   ```

## 📞 Support

- **Commands**: Check `commands/` directory
- **Agents**: Check [AGENTS_GUIDE.md](AGENTS_GUIDE.md)
- **Setup**: Check [SETUP_GUIDE.md](SETUP_GUIDE.md)
- **Project**: Check [PROJECT_PLAN.md](PROJECT_PLAN.md)

---

**Ready to build amazing tests with Claude Code!** 🚀

---

**Version**: 1.0
**Last Updated**: 2025-10-25
**Configuration Status**: ✅ Complete and Ready
