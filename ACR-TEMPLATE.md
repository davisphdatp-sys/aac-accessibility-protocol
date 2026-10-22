# Accessibility Conformance Report Template for AAC Apps

Template version 0.1.0, for use with AAC Accessibility Test Protocol version 0.1.0

License: Creative Commons Attribution 4.0 International (CC BY 4.0). See [LICENSE](LICENSE).

## About this template

"VPAT" is a registered trademark of the Information Technology Industry Council (ITI). This template follows the public structure of the VPAT 2.5 (WCAG, 508, EU, and INT editions), but it is not an official ITI document and is not endorsed by ITI. Vendors who want an official VPAT should obtain the template from ITI at <https://www.itic.org/policy/accessibility/vpat>.

This template adds AAC-specific conformance rows that map to the tests in [PROTOCOL.md](PROTOCOL.md). An Accessibility Conformance Report (ACR) completed with this template should be backed by hardware test evidence gathered under that protocol. iOS Simulator and other emulators cannot validate assistive technology, and simulator results are never accepted as evidence.

### How to use this template

1. Copy this file and replace every bracketed placeholder, such as `[Product name]`.
2. Fill in every row. Use "Not Evaluated" honestly when a criterion was not tested.
3. Cite protocol test IDs and evidence in the Remarks and Explanations column.
4. Delete this "How to use this template" subsection before publishing.

## Product information

| Field | Entry |
| --- | --- |
| Name of product | [Product name] |
| Product version and build | [Version and build number] |
| Edition | [For example, standard, school, or clinical edition, if more than one exists] |
| Report date | [YYYY-MM-DD] |
| Product description | [A short description of the AAC app, its intended users, and its supported access methods] |
| Contact information | [Name, role, email for accessibility questions] |
| Notes | [Any scope limits, for example "iPad only; iPhone not evaluated"] |
| Evaluation methods used | [For example: "AAC Accessibility Test Protocol version 0.1.0, all categories, fresh install and configured-state runs, on physical hardware listed below. Accessibility Inspector audits. Observation of two AAC users with consent."] |
| Protocol version | AAC Accessibility Test Protocol version [0.1.0] |
| Hardware used | [Device models, OS versions, switch interface class, number of switches, eye tracker class or pointing device class, audio output devices] |
| Assistive technology used | [VoiceOver, Switch Control, AssistiveTouch dwell, app's built-in scanner, app's gaze mode, and OS versions] |
| Evaluation dates | [Start date to end date] |

## Applicable standards and guidelines

This report covers the following accessibility standards and guidelines:

| Standard or guideline | Included in report |
| --- | --- |
| Web Content Accessibility Guidelines 2.2, Level A | [Yes / No] |
| Web Content Accessibility Guidelines 2.2, Level AA | [Yes / No] |
| Web Content Accessibility Guidelines 2.2, Level AAA | [Yes / No / Partially] |
| Revised Section 508 standards (36 CFR Part 1194), January 2017, corrected January 2018 | [Yes / No] |
| EN 301 549, Accessibility requirements for ICT products and services (state the version) | [Yes / No] |
| AAC Accessibility Test Protocol (state the version) | [Yes / No] |

## Terms

The terms used in the Conformance Level columns are defined as follows:

| Term | Definition |
| --- | --- |
| Supports | The functionality of the product has at least one method that meets the criterion without known defects, or meets it with equivalent facilitation. |
| Partially Supports | Some functionality of the product does not meet the criterion. |
| Does Not Support | The majority of product functionality does not meet the criterion. |
| Not Applicable | The criterion is not relevant to the product. |
| Not Evaluated | The product has not been evaluated against the criterion. This can be used only in WCAG Level AAA, or where this template explicitly allows it. In this template, Not Evaluated is also allowed in the AAC-specific rows when equipment or access was not available, with an explanation. |

Every Remarks and Explanations entry should name the protocol test IDs used, the result, and the evidence reference.

## WCAG 2.2 report

WCAG 2.2 is written for web content. For a native app, apply each criterion as described in the W3C guidance on applying WCAG to non-web information and communications technology. Success criterion 4.1.1 Parsing is obsolete and removed in WCAG 2.2; it is listed for reference only.

### Table 1: Success Criteria, Level A

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 1.1.1 Non-text Content (Level A) | [ ] | [Protocol VO-01, VO-10, HC-05] |
| 1.2.1 Audio-only and Video-only (Prerecorded) (Level A) | [ ] | [Note any tutorial or help media] |
| 1.2.2 Captions (Prerecorded) (Level A) | [ ] | [Note any tutorial or help video] |
| 1.2.3 Audio Description or Media Alternative (Prerecorded) (Level A) | [ ] | [ ] |
| 1.3.1 Info and Relationships (Level A) | [ ] | [Protocol VO-02, VO-09, VO-10] |
| 1.3.2 Meaningful Sequence (Level A) | [ ] | [Protocol VO-03, SC-02] |
| 1.3.3 Sensory Characteristics (Level A) | [ ] | [Protocol HC-06] |
| 1.4.1 Use of Color (Level A) | [ ] | [Protocol HC-04, HC-06] |
| 1.4.2 Audio Control (Level A) | [ ] | [Protocol VO-08, SC-06, EM-05, SP-03, SP-06, SP-08] |
| 2.1.1 Keyboard (Level A) | [ ] | [Protocol VO-07, SC-01, SC-03, SC-08, SC-10, EG-07, EM-03; note external keyboard support] |
| 2.1.2 No Keyboard Trap (Level A) | [ ] | [Protocol VO-04] |
| 2.1.4 Character Key Shortcuts (Level A) | [ ] | [ ] |
| 2.2.1 Timing Adjustable (Level A) | [ ] | [Protocol SC-03, SC-04, SC-05, SC-08, EG-04] |
| 2.2.2 Pause, Stop, Hide (Level A) | [ ] | [Protocol SC-05, EG-07, RM-02, SP-03] |
| 2.3.1 Three Flashes or Below Threshold (Level A) | [ ] | [Protocol RM-02] |
| 2.4.1 Bypass Blocks (Level A) | [ ] | [Protocol VO-09, EM-01, EM-02] |
| 2.4.2 Page Titled (Level A) | [ ] | [Protocol VO-06] |
| 2.4.3 Focus Order (Level A) | [ ] | [Protocol VO-03, VO-04, SC-02] |
| 2.4.4 Link Purpose (In Context) (Level A) | [ ] | [ ] |
| 2.5.1 Pointer Gestures (Level A) | [ ] | [Protocol VO-07, EG-01, EG-02, TT-05] |
| 2.5.2 Pointer Cancellation (Level A) | [ ] | [Protocol SC-09, EG-06, TT-04] |
| 2.5.3 Label in Name (Level A) | [ ] | [Compare visible cell text with VoiceOver label, VO-01] |
| 2.5.4 Motion Actuation (Level A) | [ ] | [Protocol RM-03] |
| 3.1.1 Language of Page (Level A) | [ ] | [Protocol SP-01] |
| 3.2.1 On Focus (Level A) | [ ] | [Protocol VO-06, SC-11, EG-06, SP-05] |
| 3.2.2 On Input (Level A) | [ ] | [Protocol SP-05] |
| 3.2.6 Consistent Help (Level A, new in WCAG 2.2) | [ ] | [Protocol SC-10, EM-01 to EM-04, EM-07, CC-04] |
| 3.3.1 Error Identification (Level A) | [ ] | [ ] |
| 3.3.2 Labels or Instructions (Level A) | [ ] | [Protocol EG-02, PR-05, CC-08] |
| 3.3.7 Redundant Entry (Level A, new in WCAG 2.2) | [ ] | [Note setup and editing flows] |
| 4.1.1 Parsing (obsolete and removed in WCAG 2.2) | Not Applicable | Removed in WCAG 2.2. |
| 4.1.2 Name, Role, Value (Level A) | [ ] | [Protocol VO-01, VO-02, VO-05, SC-01, SC-12, EM-02, CC-02, CC-08] |

### Table 2: Success Criteria, Level AA

The six Level A and AA success criteria added in WCAG 2.2 are 2.4.11, 2.5.7, 2.5.8, and 3.3.8 at Level AA (below), and 3.2.6 Consistent Help and 3.3.7 Redundant Entry, which are Level A and appear in Table 1.

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 1.2.4 Captions (Live) (Level AA) | [ ] | [ ] |
| 1.2.5 Audio Description (Prerecorded) (Level AA) | [ ] | [ ] |
| 1.3.4 Orientation (Level AA) | [ ] | [Protocol DT-03] |
| 1.3.5 Identify Input Purpose (Level AA) | [ ] | [Note account and setup fields] |
| 1.4.3 Contrast (Minimum) (Level AA) | [ ] | [Protocol HC-01, HC-05] |
| 1.4.4 Resize Text (Level AA) | [ ] | [Protocol DT-01, DT-02, DT-04, DT-05, CC-08] |
| 1.4.5 Images of Text (Level AA) | [ ] | [ ] |
| 1.4.10 Reflow (Level AA) | [ ] | [Protocol DT-02, DT-03, DT-05] |
| 1.4.11 Non-text Contrast (Level AA) | [ ] | [Protocol SC-07, EG-05, HC-02] |
| 1.4.12 Text Spacing (Level AA) | [ ] | [Protocol DT-02] |
| 1.4.13 Content on Hover or Focus (Level AA) | [ ] | [ ] |
| 2.4.5 Multiple Ways (Level AA) | [ ] | [ ] |
| 2.4.6 Headings and Labels (Level AA) | [ ] | [Protocol VO-01, VO-09] |
| 2.4.7 Focus Visible (Level AA) | [ ] | [Protocol SC-07, EG-05, HC-02] |
| 2.4.11 Focus Not Obscured (Minimum) (Level AA, new in WCAG 2.2) | [ ] | [Protocol DT-03] |
| 2.5.7 Dragging Movements (Level AA, new in WCAG 2.2) | [ ] | [Protocol TT-05] |
| 2.5.8 Target Size (Minimum) (Level AA, new in WCAG 2.2) | [ ] | [Protocol TT-01, TT-02, TT-03, EG-03; protocol requires 44 x 44 pt] |
| 3.1.2 Language of Parts (Level AA) | [ ] | [Protocol SP-01] |
| 3.2.3 Consistent Navigation (Level AA) | [ ] | [Protocol SC-10, SC-11] |
| 3.2.4 Consistent Identification (Level AA) | [ ] | [ ] |
| 3.3.3 Error Suggestion (Level AA) | [ ] | [ ] |
| 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA) | [ ] | [Protocol EG-08, TT-03, EM-06, SP-04, SP-09, OF-04, PR-08, CC-01 to CC-03, CC-05] |
| 3.3.8 Accessible Authentication (Minimum) (Level AA, new in WCAG 2.2) | [ ] | [Protocol OF-03, PR-01] |
| 4.1.3 Status Messages (Level AA) | [ ] | [Protocol VO-05, VO-06] |

### Table 3: Success Criteria, Level AAA

Level AAA reporting is optional. Mark criteria that were not evaluated as Not Evaluated. The protocol touches the following AAA criteria; list others if evaluated.

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 1.4.6 Contrast (Enhanced) (Level AAA) | [ ] | [Protocol HC-03] |
| 2.3.3 Animation from Interactions (Level AAA) | [ ] | [Protocol RM-01, RM-03] |
| 2.4.13 Focus Appearance (Level AAA) | [ ] | [Protocol SC-07] |
| 2.5.5 Target Size (Enhanced) (Level AAA) | [ ] | [Protocol TT-01, EG-03] |
| Other Level AAA criteria | [Not Evaluated] | [List any additional AAA criteria evaluated] |

## Revised Section 508 report

### Chapter 3: Functional Performance Criteria

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 302.1 Without Vision | [ ] | [Protocol VO category, SC-06] |
| 302.2 With Limited Vision | [ ] | [Protocol DT, HC categories] |
| 302.3 Without Perception of Color | [ ] | [Protocol HC-04, HC-06] |
| 302.4 Without Hearing | [ ] | [Note visual display of the message for deaf partners] |
| 302.5 With Limited Hearing | [ ] | [Protocol EM-05, SP-07] |
| 302.6 Without Speech | [ ] | [Core AAC function; protocol SP, OF, EM categories] |
| 302.7 With Limited Manipulation | [ ] | [Protocol SC, EG, TT categories] |
| 302.8 With Limited Reach and Strength | [ ] | [Protocol SC, EG, TT categories] |
| 302.9 With Limited Language, Cognitive, and Learning Abilities | [ ] | [Note predictability tests SP-05, SC-11, RM category] |

### Chapter 4: Hardware

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| Chapter 4 Hardware | [Not Applicable] | [Usually not applicable to a software-only AAC app. If the product is sold with a dedicated device, report Chapter 4 in full.] |

### Chapter 5: Software

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 501.1 Scope, Incorporation of WCAG 2.0 AA | [See WCAG tables] | [Section 508 incorporates WCAG 2.0 Level A and AA; the WCAG 2.2 tables above include those criteria] |
| 502.2.1 User Control of Accessibility Features | [ ] | [ ] |
| 502.2.2 No Disruption of Accessibility Features | [ ] | [Protocol VO-08, SC-12, TT-04, CC-03, SP-07] |
| 502.3.1 Object Information | [ ] | [Protocol VO-01, VO-02] |
| 502.3.2 Modification of Object Information | [ ] | [ ] |
| 502.3.3 Row, Column, and Headers | [ ] | [Grid structure exposed to assistive technology, VO-03] |
| 502.3.4 Values | [ ] | [Protocol VO-02] |
| 502.3.5 Modification of Values | [ ] | [Protocol VO-02] |
| 502.3.6 Label Relationships | [ ] | [ ] |
| 502.3.7 Hierarchical Relationships | [ ] | [Folder and page hierarchy, VO-06] |
| 502.3.8 Text | [ ] | [Message bar content, VO-05] |
| 502.3.9 Modification of Text | [ ] | [ ] |
| 502.3.10 List of Actions | [ ] | [Protocol VO-07] |
| 502.3.11 Actions on Objects | [ ] | [Protocol VO-07, SC-01] |
| 502.3.12 Focus Cursor | [ ] | [Protocol VO-03, SC-07] |
| 502.3.13 Modification of Focus Cursor | [ ] | [ ] |
| 502.3.14 Event Notification | [ ] | [Protocol VO-05, VO-06] |
| 502.4 Platform Accessibility Features | [ ] | [Not usually applicable to apps; applies to platforms] |
| 503.2 User Preferences | [ ] | [Protocol DT, RM, HC-03, SC-04, EG-04, SP-02, SP-06] |
| 503.3 Alternative User Interfaces | [ ] | [The app's built-in scanner or gaze mode, if present] |
| 503.4 User Controls for Captions and Audio Description | [ ] | [ ] |
| 504 Authoring Tools | [ ] | [Applies if the app's vocabulary editor creates content for others] |

### Chapter 6: Support Documentation and Services

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 602.2 Accessibility and Compatibility Features | [ ] | [Does documentation list accessibility features, access methods, and compatible assistive technology?] |
| 602.3 Electronic Support Documentation | [ ] | [Is the documentation itself accessible? Protocol CC-06 export format documentation] |
| 602.4 Alternate Formats for Non-Electronic Support Documentation | [ ] | [ ] |
| 603.2 Information on Accessibility and Compatibility Features | [ ] | [Does support staff provide accessibility information?] |
| 603.3 Accommodation of Communication Needs | [ ] | [Can AAC users and people with disabilities contact support in an accessible way?] |

## EN 301 549 report

Summarize EN 301 549 conformance by clause. State the version of EN 301 549 used, and check which version of WCAG it references. Clause 9 maps to WCAG for web content, and clause 11 applies equivalent requirements to software, so the WCAG tables above supply most of the evidence.

| Clause | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| Clause 4: Functional performance statements | [ ] | [Corresponds to Section 508 chapter 3 above] |
| Clause 5: Generic requirements (including 5.2 activation of accessibility features, 5.8 double-strike key acceptance, 5.9 simultaneous user actions) | [ ] | [Protocol SC-09 for double-strike acceptance] |
| Clause 6: ICT with two-way voice communication | [ ] | [Usually not applicable unless the app provides calling] |
| Clause 7: ICT with video capabilities | [ ] | [ ] |
| Clause 8: Hardware | [Not Applicable] | [Unless sold with a dedicated device] |
| Clause 9: Web | [ ] | [Applies to any web content; maps to WCAG] |
| Clause 10: Non-web documents | [ ] | [Exported files, manuals] |
| Clause 11: Software (including 11.5 interoperability with assistive technology, 11.6 documented accessibility usage, 11.7 user preferences, 11.8 authoring tools) | [ ] | [See WCAG tables and Section 508 chapter 5 above] |
| Clause 12: Documentation and support services | [ ] | [Corresponds to Section 508 chapter 6 above] |
| Clause 13: ICT providing relay or emergency service access | [ ] | [Usually not applicable; note that the protocol's EM category covers emergency vocabulary, not emergency service access] |

## AAC-specific conformance rows

These rows report results from the AAC Accessibility Test Protocol. They are not part of the VPAT 2.5 structure. Use the same conformance terms defined above. Not Evaluated is allowed here, with an explanation.

| AAC capability | Protocol test IDs | Conformance Level | Remarks and Explanations |
| --- | --- | --- | --- |
| VoiceOver labels match spoken words, focus order follows the grid | VO-01, VO-03 | [ ] | [ ] |
| VoiceOver and app speech coexist | VO-08 | [ ] | [ ] |
| Switch scanning reaches every element, in visual order | SC-01, SC-02, SC-03 | [ ] | [ ] |
| One-switch auto scan and two-switch step scan | SC-08 | [ ] | [ ] |
| Scan timing, pause, acceptance, and debounce | SC-04, SC-05, SC-09 | [ ] | [ ] |
| Auditory scanning on a separate cue channel | SC-06 | [ ] | [ ] |
| Scan highlight visibility | SC-07 | [ ] | [ ] |
| Eye gaze dwell selection, dwell range, and feedback | EG-01, EG-04, EG-05 | [ ] | [ ] |
| Gaze target size, rest area, and no selection while reading | EG-03, EG-06, EG-07 | [ ] | [ ] |
| Gaze tracker disconnect recovery | EG-08 | [ ] | [ ] |
| Touch targets at least 44 x 44 pt | TT-01, TT-03 | [ ] | [ ] |
| Emergency vocabulary reachable in two actions | EM-01 | [ ] | [ ] |
| Emergency vocabulary reachable under every access method | EM-02, EM-03 | [ ] | [ ] |
| Emergency vocabulary in Guided Access and restricted modes, and protected from deletion | EM-04, EM-06, CC-04 | [ ] | [ ] |
| Speech interruption and replay | SP-03, SP-04 | [ ] | [ ] |
| Speech language, voice consistency, and audibility with Silent or Focus | SP-01, SP-02, SP-08 | [ ] | [ ] |
| Offline operation, including voices and no login wall | OF-01, OF-02, OF-03, OF-05, EM-07 | [ ] | [ ] |
| Edit lock exists and cannot be bypassed by any access method | CC-01, CC-02, CC-03 | [ ] | [ ] |
| Vocabulary backup, restore, and data export in an open format | CC-05, CC-06 | [ ] | [ ] |
| Privacy of message history: storage, backup, deletion | PR-03, PR-04 | [ ] | [ ] |
| Network traffic matches privacy policy and label | PR-02, PR-06 | [ ] | [ ] |
| Camera and microphone consent | PR-05 | [ ] | [ ] |
| Usage logging disclosure and control | CC-07 | [ ] | [ ] |

## Evidence guidance

### What counts as evidence for each conformance level

| Conformance Level | Evidence expected |
| --- | --- |
| Supports | A completed hardware test under the cited protocol test IDs, with device model, OS version, app version, and test date, and retained screenshots, recordings, or audit exports showing the pass criterion met. |
| Partially Supports | The same hardware test record, plus a description of which functions or screens fail and the severity of each failure. |
| Does Not Support | The same hardware test record, plus a description of the failure and its severity. |
| Not Applicable | A short reason why the criterion or test does not apply to this product. |
| Not Evaluated | A short reason, such as missing equipment or out-of-scope platform. No evidence is required. |

### Evidence rules

- Every Supports claim must cite a hardware test, naming the device model, OS version, and test date. A claim based on a simulator, an emulator, a design review, or code inspection alone is not sufficient.
- Screenshots, screen recordings, and audit exports should be retained for as long as the report is in use, and offered to purchasers on request.
- "Not Evaluated" is an honest and allowed answer. It is better than a claim that was not tested.
- Do not make a conformance statement about an assistive technology that was not actually tested. For example, do not claim eye gaze support if no eye tracker or pointing device was used with the product.
- If results differ between devices or OS versions, report each separately in the Remarks and Explanations column.
- Name evidence files using the protocol's convention: `TESTID_app_version_device_os_date.ext`.
- Remove personal information about any participant from shared evidence.

## Example remarks

The rows below are fictional examples of well-formed remarks. They describe no real product.

| Criteria | Conformance Level | Remarks and Explanations |
| --- | --- | --- |
| 2.5.8 Target Size (Minimum) (Level AA) | Partially Supports | Protocol TT-01 and TT-03, tested 2026-10-14 on an iPad (10th generation), iPadOS 26.1, app version 2.3.1. All cells meet 44 x 44 pt at grid sizes up to 6 x 8. At the densest grid (10 x 12) cells measure 38 x 38 pt and no warning is shown (TT-03 Fail, Major). Evidence: TT-03_appname_2.3.1_iPad-10th-gen_iPadOS-26.1_2026-10-14.png. |
| Emergency vocabulary reachable under every access method | Supports | Protocol EM-02 and EM-03, tested 2026-10-15 on the same device with VoiceOver, iPadOS Switch Control (one switch, auto scan at 1.5 seconds), and AssistiveTouch dwell with an external pointing device. The help area is the first scan group on every page and the first VoiceOver element after the message bar. Evidence retained and available on request. |
| Eye gaze dwell selection, dwell range, and feedback | Not Evaluated | No eye tracker was available to the evaluator. No claim is made about eye gaze support. |

## Report sign-off

| Field | Entry |
| --- | --- |
| Evaluator name | [Name] |
| Evaluator role and credentials | [Role, credentials] |
| Organization | [Organization] |
| Date signed | [YYYY-MM-DD] |
| Independence statement | [Select one: "The evaluator is the vendor or is employed by the vendor." / "The evaluator is an independent third party with no financial relationship with the vendor." / "The evaluator is a purchaser or prospective purchaser." Disclose any other relationship.] |
| Protocol version used | AAC Accessibility Test Protocol version [0.1.0] |
| Statement | [Optional: "The results in this report reflect testing on physical hardware as described above, on the dates listed."] |

## Revision history

| Report version | Date | Changes |
| --- | --- | --- |
| [1.0] | [YYYY-MM-DD] | [Initial report] |

Template based on the AAC Accessibility Test Protocol by Dr. Jeffrey Davis, PhD, ATP, licensed under CC BY 4.0.
