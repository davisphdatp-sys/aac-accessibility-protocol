# AAC Accessibility Test Protocol

Version 0.1.0 (draft for public comment), October 2026

Author: Dr. Jeffrey Davis, PhD, ATP

The AAC Accessibility Test Protocol is an open, vendor-neutral, hardware-based test protocol for checking the accessibility, safety, privacy, and reliability of augmentative and alternative communication (AAC) apps on iPad and iPhone. It gives evaluators a set of specific, repeatable tests with stable IDs, clear pass and fail criteria, and rules for recording evidence. The repository also includes an Accessibility Conformance Report (ACR) template tailored to AAC apps and a one-page procurement checklist for school districts. The protocol rates no products and makes no claims about any product: it describes how to test, and it leaves the testing to you.

## Who this is for

- **School districts and procurement teams** who need evidence, not marketing claims, before buying an AAC app for students.
- **Speech-language pathologists (SLPs) and clinicians** who match AAC apps to a person's access method and want a structured way to check that the app actually works with that access method.
- **Families and self-advocates** who want to know what questions to ask and what to try on their own device before relying on an app.
- **Developers** who build AAC apps and want a public, testable definition of what accessible, safe, and private AAC software looks like.

## What is in this repository

| File | Description |
| --- | --- |
| [PROTOCOL.md](PROTOCOL.md) | The full test protocol: scope, hardware requirement, test procedure, every test by category, reporting, and change control. |
| [ACR-TEMPLATE.md](ACR-TEMPLATE.md) | An Accessibility Conformance Report template for AAC apps, following the public structure of VPAT 2.5, with AAC-specific rows. |
| [PROCUREMENT-CHECKLIST.md](PROCUREMENT-CHECKLIST.md) | A one-page checklist for school districts buying an AAC app. |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to propose changes, submit test results, and follow the house style. |
| [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) | Community standards for everyone who takes part in this project. |
| [SECURITY.md](SECURITY.md) | How to report a security or privacy concern about this repository. |
| [ACCESSIBILITY.md](ACCESSIBILITY.md) | The accessibility commitment for this repository and its documents. |
| [.github/ISSUE_TEMPLATE](.github/ISSUE_TEMPLATE) | Issue templates for submitting test results, proposing protocol changes, and reporting bugs in the documents. |
| [LICENSE](LICENSE) | The Creative Commons Attribution 4.0 International license text. |

## How to run the protocol

The full procedure is in [PROTOCOL.md](PROTOCOL.md). This section is a short orientation.

### Physical hardware only

iOS Simulator and other emulators cannot validate assistive technology. They do not reproduce VoiceOver, Switch Control, eye gaze, physical switches, or real speech output timing. Every test in this protocol is run on physical hardware. A simulator result is never accepted as evidence.

### Hardware you need

- A physical iPad, iPhone, or both, running a current supported version of iPadOS or iOS.
- At least one switch interface (for example, a Bluetooth switch interface) and at least one physical switch. Two switches are needed for two-switch step scanning tests.
- A USB or Bluetooth eye tracker, if you are testing eye gaze and dwell.
- Headphones or an external speaker (wired or Bluetooth) for speech output routing tests.
- A Mac with Xcode installed, if you want to run Accessibility Inspector audits.
- A second person to observe and record, when possible.

Not every test needs every item. The equipment table in [PROTOCOL.md](PROTOCOL.md) lists which tests need which hardware. If you do not have the equipment for a test, record it as Blocked or Not Evaluated, never as Pass.

### How to record evidence

- **Screenshots** that show the whole screen, not a cropped region.
- **Screen recordings with audio** for any test that involves speech output, VoiceOver announcements, or auditory scanning.
- **Accessibility Inspector audit exports**, when the app can be inspected from a connected Mac.
- **Written observations** describing exactly what happened, in plain language, including the device model, OS version, app version, and date.

Name evidence files using the convention in [PROTOCOL.md](PROTOCOL.md), for example `VO-01_appname_2.3.1_iPad-10th-gen_iPadOS-26.1_2026-10-21.png`.

### How to submit results

Open a new issue using the test result issue template in [.github/ISSUE_TEMPLATE](.github/ISSUE_TEMPLATE). List every test you ran, including tests that were Not Applicable or Blocked, with a reason. Attach or link your evidence files.

Results are observations, not endorsements. A submitted result records what one evaluator observed on one device, with one app version, on one date. It is not a rating, a certification, or a recommendation, and this project does not publish rankings or scores.

## Test ID scheme

Every test has a stable ID made of a two-letter category code and a two-digit number, for example `VO-01`. IDs are never reused. If a test is retired, its ID stays retired.

| Code | Category |
| --- | --- |
| VO | VoiceOver |
| SC | Switch Control and in-app scanning |
| EG | Eye gaze and dwell |
| TT | Touch targets |
| DT | Dynamic Type |
| RM | Reduce Motion |
| HC | High contrast and color independence |
| EM | Emergency and safety vocabulary |
| SP | Speech output |
| OF | Offline operation |
| PR | Privacy |
| CC | Clinician and caregiver controls |

Tests are numbered VO-01, VO-02, and so on within each category. The issue templates use the same category codes.

## What this protocol is not

- **Not a rating system.** Results are recorded per test as Pass, Fail, Not Applicable, or Blocked. They are never added up into a score, a grade, or a ranking.
- **Not a certification.** No one can be "certified" against this protocol, and no badge or seal is offered.
- **Not a substitute for a feature-match evaluation.** Choosing an AAC system for a person is a clinical process led by the person, their family, and qualified professionals. This protocol checks whether an app works with a given access method; it does not decide which app is right for someone.
- **Not legal advice.** The privacy tests include a checklist of student privacy laws to consider. Districts should consult their own counsel.

## Quick start for a first evaluation

If you are new to the protocol, a short first pass covers the tests where failures cause the most harm:

1. Read sections 1 to 3 of [PROTOCOL.md](PROTOCOL.md), including the result and severity definitions.
2. Install the app on a physical iPad or iPhone and complete initial setup. Note the app version, device model, and OS version.
3. Run the Emergency and safety vocabulary tests (EM) under the student's actual access method.
4. Run the access method category that matches the student: VoiceOver (VO), Switch Control and in-app scanning (SC), or Eye gaze and dwell (EG).
5. Run the Speech output (SP) and Offline operation (OF) tests.
6. Run the Privacy (PR) and Clinician and caregiver controls (CC) tests.
7. Run the remaining categories (TT, DT, RM, HC) when time allows.
8. Record every test you ran and every test you skipped, with a reason, using the reporting table in section 5 of [PROTOCOL.md](PROTOCOL.md).

A short first pass is still a partial evaluation. Label it as partial in your report.

## Standards referenced

- **WCAG 2.2**, Web Content Accessibility Guidelines, from the W3C: <https://www.w3.org/TR/WCAG22/>. WCAG is written for web content, but its success criteria are widely applied to native mobile apps, including by Section 508 and EN 301 549.
- **Apple Human Interface Guidelines, Accessibility**: <https://developer.apple.com/design/human-interface-guidelines/accessibility>.
- **Apple accessibility developer documentation**, including the documentation for UIAccessibility, SwiftUI accessibility modifiers, and Accessibility Inspector: <https://developer.apple.com/accessibility/>.
- **VPAT 2.5**, the Voluntary Product Accessibility Template from the Information Technology Industry Council (ITI): <https://www.itic.org/policy/accessibility/vpat>. VPAT is a registered trademark of ITI.
- **Revised Section 508 Standards** (36 CFR Part 1194), United States: <https://www.access-board.gov/ict/>.
- **EN 301 549**, Accessibility requirements for ICT products and services, European standard.

## Frequently asked questions

### Can I run the protocol without a switch or an eye tracker?

Yes. Run the tests you have equipment for and record the others as Blocked, with the reason "equipment not available". Do not record a test as Pass unless you ran it on physical hardware with the required equipment.

### Does a vendor's own test report count?

A vendor may run this protocol on its own product and publish the results. The ACR template asks every evaluator to state whether they are the vendor, an independent third party, or a purchaser, so readers can weigh the evidence accordingly.

### What if a test does not fit the app I am evaluating?

Record the test as Not Applicable and explain why. If you think the test itself is wrong or unclear, open an issue with the protocol change template.

### Does this protocol cover AAC apps on other platforms?

Version 0.1.0 covers iPadOS and iOS only, because the settings paths and platform features named in the tests are specific to those systems. Many tests translate to other platforms, and proposals for platform supplements are welcome.

## How to contribute

Contributions are welcome: new tests, clearer steps, corrections, translations, and test results. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request. In short:

- Propose protocol changes through the protocol change issue template before writing them.
- Keep the protocol vendor-neutral. Do not name AAC products, companies, or hardware brands. Describe device classes generically.
- House style: do not use long dashes (em dashes or en dashes). Use commas, colons, periods, parentheses, or the word "to" for ranges. Plain ASCII hyphens are fine.
- Commit messages must not include AI attribution trailers (for example, "Co-Authored-By" lines naming an AI tool). Write a plain, descriptive commit message in your own name.
- All contributions are licensed under CC BY 4.0, the same license as the rest of the repository.

## Disclosure

Disclosure: the author is the founder of EquaAccess, which makes an AAC app. This protocol is vendor-neutral and rates no products. It was written from public standards and first principles, and it contains no material from any product.

## License

This work is licensed under the Creative Commons Attribution 4.0 International License (CC BY 4.0). See [LICENSE](LICENSE) for the full text, or read the license summary at <https://creativecommons.org/licenses/by/4.0/>.

You may copy, adapt, and redistribute this protocol for any purpose, including commercially, as long as you give credit. Please attribute it as:

```text
AAC Accessibility Test Protocol by Dr. Jeffrey Davis, PhD, ATP, licensed under CC BY 4.0
```

If you adapt the protocol, say that you changed it, and link to the license.

## Status

Version 0.1.0 (draft for public comment), October 2026
