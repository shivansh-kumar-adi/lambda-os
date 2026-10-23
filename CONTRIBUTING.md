# Contributing

Thank you for looking at ΛOS. This repository is documentation only, and the source is not published, so contributions here are about accuracy and clarity.

## Useful contributions

- Corrections to technical explanations (x86-64, paging, exceptions, boot).
- Broken links, typos and unclear writing.
- Diagram clarity improvements.

## Ground rules

1. Keep claims honest. Do not mark something as working unless the evidence supports it.
2. Keep status labels consistent: Reported working, Experimental, Planned, Open decision.
3. Do not add source code, secrets, tokens, personal data or machine-specific paths.
4. Diagram sources live in `docs/architecture/` as Mermaid. Update the rendered images in `assets/diagrams/` when you change a source.
5. Run the validators before proposing a change:
   - `scripts/validate_showcase.py` checks for forbidden files and obvious credentials.
   - `scripts/validate_links.py` checks that relative Markdown links resolve.

## Process

Open an issue to discuss larger changes, then send a pull request from a branch. By contributing you agree your changes may be distributed under the repository license (CC BY-NC-ND 4.0), which applies to documentation only.

Security-related findings: see [SECURITY.md](SECURITY.md).
