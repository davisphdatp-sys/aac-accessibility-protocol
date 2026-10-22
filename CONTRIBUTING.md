# Contributing to the AAC Accessibility Test Protocol

Thank you for your interest in improving this protocol. Contributions from users, clinicians, evaluators, and developers make this resource valuable for the entire AAC community.

## How to Propose a Protocol Change

Before submitting code or documentation, please open a protocol-change issue first. This allows the maintainers and community to discuss your proposal.

### In Your Issue

Describe the user need: which AAC users and access method does your change serve? For example, "this clarifies testing for users who rely on eye-gaze access."

Explain the standard it maps to: reference the applicable WCAG 2.2 success criterion (such as WCAG 2.2 section 2.1.1 Keyboard) or platform guideline (such as iOS Accessibility Guidelines for Motor).

Propose the test text or wording change. For new tests, use this seven-field layout:

- Setup: conditions before starting
- Steps: actions the tester performs
- Expected result: what should happen
- Pass criterion: objective way to measure passing
- Fail criterion: objective way to measure failing
- Evidence to record: documentation the tester captures
- Maps to: the standard (WCAG criterion, platform guideline, or accessible design principle)

Important: test IDs are stable. Once assigned (VO-01, SC-02, etc.), they are never reused. If a test changes significantly, the ID stays the same. If a test is removed, the ID is marked deprecated, not reassigned.

### Community Discussion

Link to relevant research, observed failures in real-world usage, or standards documents that support the change. The maintainers will engage with your proposal in the issue thread.

## How to Submit Test Results

Test results are submitted via test-result issue. This creates a public record of how apps perform and helps identify patterns.

### Requirements

Results come from a physical device only. Simulator results are not accepted because simulators do not reproduce the behavior of assistive technologies (such as switch scanning, eye-gaze calibration, or VoiceOver tracking) with sufficient accuracy.

Do not include personal information, children's faces, or user names in evidence. Screenshots and recordings should show only the app UI and test results.

Include in your submission:

- App name and version
- Device model and OS version
- Date tested
- Your role (developer, clinician, evaluator, family member, etc.)
- Which test categories you ran (VoiceOver, Switch Control, Dynamic Type, etc.)
- Results for each test (Pass, Fail, Not Applicable, or Blocked)
- Severity of each failure (Critical, Major, Minor)
- Supporting evidence (screenshots, recordings, or notes)

Results are observations about how an app performed under the test protocol. Submitting a result is not an endorsement of the app or guarantee of accessibility.

## House Style

Keep contributions clear and accessible:

- Use plain language and short sentences.
- Do not use em dashes (-) or en dashes (-). Use commas, colons, periods, or parentheses instead.
- Use straight quotes ("like this"), not curly quotes.
- Each Markdown file has exactly one H1 heading at the top.
- Headings are in order without skipped levels (H1, then H2, then H3, etc.).
- Images include meaningful alt text that describes what the image shows and why it matters.
- Links have descriptive text ("See the PROTOCOL.md file") instead of bare URLs or "click here."
- Line length is free; prioritize readability.

All Markdown files must pass markdownlint default rules (with line-length and inline-HTML rules disabled).

## Pull Request Process

Keep pull requests small and focused. One fix or feature per PR helps maintainers review and merge efficiently.

### Before You Submit

Enable the git hook that protects against AI attribution trailers:

```bash
git config core.hooksPath .githooks
```

### Checklist for Your PR

- [ ] I have one H1 per file and no skipped heading levels.
- [ ] Tables have header rows and no merged cells.
- [ ] Every image has meaningful alt text.
- [ ] All links have descriptive text (no "click here" or bare URLs).
- [ ] No information is conveyed by color alone.
- [ ] I used no em or en dashes; only commas, colons, periods, or hyphens.
- [ ] My Markdown passes markdownlint locally (run `markdownlint-cli2 '**/*.md'`).
- [ ] My commit messages are plain text with no "Co-Authored-By" trailers.

### Vendor Neutrality

The protocol itself must not name, rate, compare, or favor any specific app or device. Contributions must be vendor-neutral.

Results issues may name an app when reporting that app's test results, but protocol text must not do so. For example:

- OK in a test-result issue: "VoiceOver test result for [app name] version 2.1"
- Not OK in PROTOCOL.md: "This test is designed for [app name]"

## Licensing

By contributing to this repository, you agree that your contributions are licensed under the same CC BY 4.0 license as the protocol itself. You retain the right to use your contribution elsewhere, but the protocol and this repository may use it freely.

## Code of Conduct

Please read and follow the CODE_OF_CONDUCT.md file. This is a respectful community that welcomes people from all backgrounds and experiences.

## Questions?

Open a discussion in the repository Discussions tab, or email the maintainers.
