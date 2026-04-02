---
description: "Build an HTML prototype from a Figma design URL using the full 7-stage agent pipeline (extract → annotate → build → review → fix → publish → commit)."
agent: orchestrator
---

Build a production-quality HTML prototype from the given Figma URL.

Use the full pipeline: extract the design with @figma-reader, annotate tokens with @design-system-guardian, build with @ui-developer, review with @qa-reviewer, fix any issues, publish with @env-host, and commit to GitHub with @github-manager.

The prototype must use ONLY the design system specified in .github/copilot-instructions.md — zero forbidden tokens allowed.
