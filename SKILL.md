---
name: qa-istqb-skill
description: Expert QA skills for efficient test case design and Playwright automation
---

# QA ISTQB Skill

Expert QA skills for efficient test case design and Playwright automation.

## Skills Included

This package contains two specialized agent skills:

### 1. QA Senior ISTQB - Efficient Test Case Designer
Generate consolidated, efficient test cases with minimum quantity and maximum coverage.

**File:** `.claude/qa-senior-istqb.md`

**Use when:** Designing manual test cases from requirements, code, or acceptance criteria

**Key features:**
- Consolidates related validations (1 test case validates 2-4 flows)
- Targets 3-7 cases for typical features (not 15-20)
- Applies ISTQB techniques silently
- Prioritizes by risk
- Suggests critical gaps only

### 2. Playwright Automation - Code Generator
Transform test cases into clean, efficient Playwright automation code.

**File:** `.claude/playwright-automation.md`

**Use when:** Automating test cases with Playwright

**Key features:**
- Clean, maintainable code
- Stable selectors (testid > role > label)
- Minimal explanations
- Auto-waiting patterns
- Best practices built-in

## Installation

### Using npx skills CLI

```bash
npx skills add https://github.com/jsazo-bit/qa-istqb-skill
```

This will install both skills into your agent's skills directory.

### Manual Installation

```bash
git clone https://github.com/jsazo-bit/qa-istqb-skill.git
cd qa-istqb-skill
```

Then reference the skills in your prompts:
```
@.claude/qa-senior-istqb.md
```

## Quick Start

### Generate Test Cases

```
@.claude/qa-senior-istqb.md

Feature: User login
- Email and password validation
- Session management
- Remember me option
```

### Generate Playwright Code

```
@.claude/playwright-automation.md

TC-001: Login with valid credentials
1. Navigate to /login
2. Enter email: test@example.com
3. Enter password: Pass123!
4. Click "Sign In"
Expected: Redirect to /dashboard
```

## Documentation

- 📖 [Installation Guide](INSTALLATION.md) - Detailed setup instructions
- 🎓 [Team Onboarding](TEAM-ONBOARDING.md) - 15-minute onboarding guide
- 📚 [Usage Guide](USAGE.md) - Complete usage documentation
- 🚀 [Quick Start](QUICKSTART.md) - Get started in 3 steps

## Examples

See [example-senior-qa-output.md](scripts/example-senior-qa-output.md) for:
- Password validation (4 consolidated cases vs 17 atomic)
- E-commerce checkout (3 cases vs 12+)
- Before/after comparisons
- Execution time savings

## Requirements

- Visual Studio Code (1.85+)
- GitHub Copilot extension
- Git

## Philosophy

**Quality over quantity. Speed over exhaustiveness.**

These skills are optimized for QA teams that:
- Validate projects quickly and move to the next
- Need consolidated test cases, not exhaustive lists
- Want maximum coverage with minimum test cases
- Value execution speed and maintainability

## Target Metrics

- **Simple feature**: 2-3 test cases
- **Medium feature**: 3-5 test cases
- **Complex feature**: 5-8 test cases
- **Time savings**: 60-75% reduction in test execution

## Support

- [GitHub Issues](https://github.com/jsazo-bit/qa-istqb-skill/issues)
- [Documentation](https://github.com/jsazo-bit/qa-istqb-skill)

## License

MIT

## Author

jsazo-bit

## Contributing

Contributions welcome! Please read the contribution guidelines before submitting PRs.
