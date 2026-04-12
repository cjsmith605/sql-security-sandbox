# Contributing to SQL Security Sandbox

Thank you for your interest in contributing to the SQL Security Sandbox. This project aims to provide high-quality, interactive SQL training for cybersecurity professionals.

## How to Contribute

### Reporting Bugs
- Open a [GitHub Issue](../../issues) with a clear title and description
- Include your browser name/version and OS
- Describe the expected vs. actual behavior
- Screenshots or screen recordings are welcome

### Suggesting Features
- Open a [GitHub Issue](../../issues) with the label `enhancement`
- Describe the use case and how it benefits learners
- Reference any relevant cybersecurity frameworks (NIST, MITRE ATT&CK) if applicable

### Submitting Code Changes
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature-name`)
3. Make your changes to `index.html` or companion files
4. Test in at least two browsers (Chrome + Firefox recommended)
5. Test responsive layout at 360px, 768px, and 1200px widths
6. Verify keyboard navigation works on all interactive elements
7. Commit with a descriptive message (`git commit -m "Add: brief description"`)
8. Push and open a Pull Request

### Content Contributions
If you'd like to contribute new lessons or exercises:
- Follow the existing lesson data structure in the `lessons` array
- Include at least 2 exercises per lesson page
- Write regex checks that validate the key SQL concepts, not exact syntax
- Provide meaningful hints and detailed answer explanations
- Map the lesson to a NIST CSF 2.0 function if applicable

## Code Style
- This project intentionally uses **vanilla JavaScript** — no frameworks, no build step
- Keep the single-file architecture for `index.html`
- Use CSS custom properties (variables) defined in `:root`
- Follow existing naming conventions for CSS classes and JS functions
- Escape all user-controlled strings before any `innerHTML` write

## Code of Conduct
Be respectful, constructive, and professional. Discrimination, harassment, and bad-faith contributions will not be tolerated.
