# Generate Playwright Tests from Test Cases

## Input
Provide one or more of:
- Manual test case(s)
- User story acceptance criteria
- Feature specification
- Existing test scenario description

## Instructions
Transform the provided test cases into Playwright automation code following the **Playwright Automation skill**.

## Constraints
- **Efficient code**: No redundancy
- **Clean structure**: Easy to read and maintain
- **Minimal explanation**: Let code be self-documenting
- **Proper selectors**: Follow selector priority (testid > role > label > text)
- **Auto-waiting**: Leverage Playwright's built-in waiting
- **Clear assertions**: Validate expected behavior explicitly

## Output
Generate ready-to-use Playwright test code with:
1. Brief context (1-2 lines)
2. Clean test code
3. Key decisions (only if non-obvious, max 3 bullets)
