---
mode: ask
description: "Generate a JIRA issue description from notes or file"
---

Analyze the provided notes (either as text or from a file reference) and generate a well-formatted JIRA issue description.

Input: Notes about the issue or file reference

Based on the input, extract and format information into this structure:

```markdown
## Background
-

## Proposed solution
-

## Acceptance criteria
-

## FILLED BY THE DEVELOPER WHEN CREATING PR:

### Testable by QA
- Yes/No

### Extra info? (i.e. Steps to reproduce & edge cases)
- <Add any extra info useful for QA or leave empty if not applicable>
- <Provide detailed steps to reproduce or leave empty if not applicable>
- <Include any specific configurations, edge cases, data needed for testing or leave empty if not applicable>

### Regression?
- If change may affect other parts of a system or another feature, include information on what may be affected so that the QA can perform a regression test
- N/A if not applicable
```

Instructions:
1. Analyze the provided notes to identify:
   - Background/context of the issue
   - Proposed solution or approach
   - Success criteria or expected outcomes
   - Any QA-related information
   - Potential regression impacts

2. Format the extracted information into the template above
3. Fill in reasonable defaults where information is missing
4. Ensure the description is clear, professional, and actionable
5. If the notes mention testing, QA steps, or edge cases, include them in the appropriate section
