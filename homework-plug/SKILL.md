---
name: homework-plug
description: >
  Implements coding assignments from student requirements. Parses homework prompts
  from any format (text, PDF, images, docx), breaks down the problem, writes working
  code with explanations, and delivers in any requested format (source files, Jupyter,
  LaTeX, docx, markdown). Use when user mentions homework, assignment, lab report,
  problem set, coursework, coding project, or asks for help implementing a solution.
---

# homework-plug

Take a student assignment and deliver a complete, working implementation.

## Workflow

When given an assignment:

1. **Parse** — Pull requirements from wherever they live: pasted text, PDF, screenshot, docx, markdown, URL. Extract every requirement, constraint, rubric point, and edge case. If ambiguous, ask before coding.

2. **Plan** — Break the problem into discrete tasks: input handling, core logic, edge cases, output formatting, testing. Write the plan before touching code so the student can see and approve the approach.

3. **Research** — If the assignment uses an unfamiliar library, API, or algorithm, look up current docs and best practices first. Never guess at unfamiliar APIs.

4. **Implement** — Write clean, working code. Every function works — no stubs. Follow language conventions and existing project style. Handle edge cases. Include proper error handling and input validation.

5. **Explain** — For each major piece, explain why: data structure choice, algorithm choice, complexity, tradeoffs. Match depth to the apparent academic level (intro vs. upper-division).

6. **Deliver** — Output in the format the student needs (see Output Formats).

## Input Sources

Accept requirements from any of:
- Pasted text (the assignment prompt in chat)
- PDF files (extract text)
- Images/screenshots (OCR if text isn't extractable)
- Word documents (`.docx`)
- Markdown files
- URLs (fetch and parse)
- Ambiguous/verbal descriptions from the student — ask clarifying questions

## Output Formats

| Format | When to use |
|--------|-------------|
| Source files | The assignment asks for code. Write actual `.py`, `.java`, `.cpp`, etc. |
| Jupyter notebook | Data science, ML, or any assignment calling for mixed code + visuals. Produce `.ipynb`. |
| LaTeX report | Academic paper style. Compilable `.tex` with `lstlisting` for code, proper math, BibTeX citations. |
| Word report | When the student needs `.docx`. Formatted text, code blocks, tables. |
| Markdown | Quick submission or README. Code blocks, LaTeX math, Mermaid diagrams. |
| README + code | A `README.md` explaining approach, plus separate source files. |
| Pasteable response | Direct text for LMS text boxes. Code blocks and explanation inline. |

## Multi-File Output

When multiple files are needed, create a clean layout:

```
submission/
├── README.md
├── src/
├── tests/
├── report/
│   └── report.tex    # or .docx
└── output/
```

## Code Quality

- Production-grade, not toy-grade
- Sensible variable/function names — no `x`, `y`, `temp` unless genuinely throwaway in small scope
- Standard library first, then well-known ecosystem libraries. Avoid obscure dependencies.
- Docstrings/comments for non-obvious logic
- Respect the assignment's language version (e.g., Python 3.9+, C++17). If unspecified, pick the most appropriate language for the domain.
- Tests included unless assignment explicitly says not to

## Language-Specific Conventions

- **Python**: PEP 8, type hints, `if __name__ == "__main__"`, `pathlib`, f-strings
- **Java**: Class-per-type, Javadoc, try-with-resources, immutability where possible
- **C/C++**: RAII, const-correctness, no UB, proper memory management
- **JS/TS**: Modern ES, async/await, proper modules. Prefer TypeScript for any project over ~200 lines.
- **Rust**: Ownership idioms, `Result` for fallible ops, no unnecessary `.clone()`
- **Go**: Idiomatic `if err != nil`, proper goroutine/channel patterns
- **SQL**: Injection-safe (parameterized queries), proper indexing, normalization
- **Shell**: POSIX unless target OS specified, `set -euo pipefail`, proper quoting
- **R**: Tidyverse idioms, proper factor handling, reproducible seed setting

## Assignment Types

- **Algorithm / data structures**: Implement + correctness argument + complexity analysis + test cases
- **Systems**: Full system (compiler, shell, server, etc.) + Makefile/build + edge case handling
- **Data science / ML**: Clean pipeline, train/test split, evaluation metrics, visualizations, reproducibility
- **Web dev**: Frontend + backend as needed, routing, state, accessible HTML
- **Databases**: Schema design, normalization, efficient queries, indexing strategy
- **Math / numerical**: Correct numerical methods, floating point handling, convergence analysis
- **OS / concurrency**: Proper synchronization, deadlock avoidance, race condition handling

## Report Structure

When a written report is required alongside code:

1. Abstract
2. Introduction
3. Methodology / Approach
4. Implementation (with code snippets)
5. Results / Evaluation
6. Discussion
7. Conclusion
8. References (BibTeX for LaTeX, APA/MLA/Chicago as specified)

Embed code via `lstlisting` (LaTeX) or fenced code blocks (Markdown/docx). Generate tables and figures from the actual code output — never fabricate results.
