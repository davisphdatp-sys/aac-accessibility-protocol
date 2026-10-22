# AAC Accessibility Test Protocol

Version 0.1.0 (draft for public comment), October 2026

Author: Dr. Jeffrey Davis, PhD, ATP

License: Creative Commons Attribution 4.0 International (CC BY 4.0). See [LICENSE](LICENSE) and <https://creativecommons.org/licenses/by/4.0/>.

## Contents

- [1. Scope and principles](#1-scope-and-principles)
- [2. Hardware requirement](#2-hardware-requirement)
- [3. How to run a test](#3-how-to-run-a-test)
- [4. Test categories](#4-test-categories)
- [5. Reporting](#5-reporting)
- [6. Change control](#6-change-control)
- [Appendix A: WCAG 2.2 success criteria referenced](#appendix-a-wcag-22-success-criteria-referenced)
- [Appendix B: Settings paths](#appendix-b-settings-paths)
- [Appendix C: Glossary](#appendix-c-glossary)

## 1. Scope and principles

### What AAC apps are

Augmentative and alternative communication (AAC) apps are symbol-based and text-based communication apps used by people who cannot rely on speech to be understood. A typical AAC app presents a grid of cells. Each cell shows a symbol, a word, or both. Selecting cells builds a message in a message bar, and the app speaks words or the whole message aloud with synthesized or recorded speech. Some AAC apps are keyboard-based and use word prediction. People use AAC apps by direct touch, by VoiceOver, by one or two switches, by eye gaze, by head pointing, or by a combination of these.

This protocol applies to AAC apps running on iPadOS and iOS. It covers accessibility, safety, privacy, and reliability.

### Why AAC has stricter needs than general apps

For most apps, an accessibility failure means a task is harder or impossible. For an AAC app, the app is the user's voice. A failure is a loss of communication. A person who cannot reach the word "stop" or "pain" because a scan order skips the emergency area, or because a dialog traps VoiceOver focus, has lost the ability to say something that matters, possibly in an emergency. A person whose message history leaks has had their private speech exposed. For this reason, this protocol sets some requirements above general guidance (for example, a 44 point minimum touch target rather than the 24 CSS pixel minimum in WCAG 2.5.8) and adds requirements that general standards do not address at all (emergency vocabulary reachability, speech interruption, edit locks).

### Principles

1. **Hardware only.** Every test is run on a physical iPad or iPhone with real assistive technology and real accessories. Simulators and emulators are never accepted. See [section 2](#2-hardware-requirement).
2. **The user's access method is the test condition.** An app that works by touch but fails under Switch Control has failed for a switch user. Where a test names an access method, it must be run with that access method actually turned on and actually used.
3. **Observe real users where possible, with consent.** Tests can be run by an evaluator alone, but observing an AAC user who is willing to take part, with their informed consent (and a guardian's consent where required), reveals problems that a script misses. Never pressure a user to take part, never record a user without consent, and stop if the user is distressed.
4. **Record evidence.** Every result is backed by screenshots, screen recordings, audit exports, or written observations. A result without evidence is recorded as Not Evaluated.
5. **Report observations, not opinions.** Describe what happened ("VoiceOver read 'img_0042.png' for the cell showing a cup") rather than judgments ("labels are bad").
6. **Pass or fail is per test, not aggregated.** This protocol produces no score, grade, percentage, or ranking. A single Critical failure is not offset by passes elsewhere.

### Out of scope

- Choosing the right AAC system for a person. That is a clinical decision made with the person, their family, and qualified professionals.
- Language and vocabulary design quality (for example, the choice of core vocabulary), except where it affects safety or access.
- Rating, ranking, or certifying any product.
- Legal advice. The privacy tests list legal frameworks for the reviewer to consider; they do not interpret the law.

## 2. Hardware requirement

iOS Simulator and other emulators cannot validate assistive technology. They do not run VoiceOver as a user experiences it, they do not support Switch Control with physical switches, they do not support eye trackers or dwell control, and they do not reproduce real speech output timing, audio routing, or the Silent switch. Every test in this protocol is run on physical hardware. A simulator result is never accepted as evidence, for any test, under any circumstances.

### Required equipment

| Item | Required for | Notes |
| --- | --- | --- |
| Physical iPad or iPhone on a current supported iPadOS or iOS version | All tests | Record model, OS version, and storage free. Test on the device class the user will actually use. |
| Switch interface (Bluetooth or USB) | SC, EM-03, CC-03 | Any interface that presents switch input to iPadOS Switch Control or to the app's own scanner. |
| At least one physical switch; two for step scanning | SC, EM-03, CC-03 | One switch for auto scan tests, two switches for step scan tests. |
| USB or Bluetooth eye tracker, or an external pointing device supported by AssistiveTouch | EG, EM-03, CC-03 | Required only if eye gaze is in scope. If not available, record EG tests as Blocked. |
| Wired headphones, Bluetooth headphones, or a Bluetooth speaker | SP-07, SC-06 | At least one wired or Bluetooth output device for routing tests. |
| Mac with Xcode (for Accessibility Inspector) | VO-01, VO-02, TT-01, HC-01, HC-02 | Accessibility Inspector can inspect apps on a connected device. Optional but strongly recommended. |
| Color contrast analyzer (any tool that reads pixel colors from a screenshot) | HC | Any contrast checker that implements the WCAG relative luminance formula. |
| Network proxy or traffic inspection tool, or the device's per-app data usage view | PR-02 | A proxy gives a host list; the data usage view gives only totals. |
| Second device or camera for filming the screen and the tester | Optional | Useful when screen recording cannot capture an external accessory's behavior. |
| A second person (observer) | Recommended | See tester roles in [section 3](#3-how-to-run-a-test). |

### Which tests need which equipment

- **Device only:** VO, TT, DT, RM, HC, EM-01, EM-02, EM-04 to EM-07, SP-01 to SP-06, SP-08, SP-09, OF, PR (except PR-02 with a proxy), CC (except CC-03).
- **Switch interface and switches:** all SC tests, plus the switch portions of EM-03 and CC-03.
- **Eye tracker or external pointing device:** all EG tests, plus the gaze portions of EM-03 and CC-03.
- **Audio output devices:** SP-07, and the separate-channel portion of SC-06.
- **Mac with Accessibility Inspector:** recommended for VO-01, VO-02, and TT-01.

If equipment for a test is not available, record the result as Blocked and state what was missing.

## 3. How to run a test

### Environment setup

Run the protocol twice where practical:

1. **Fresh install run.** Delete the app, restart the device, install the app from its normal distribution channel, and complete the app's first-run setup with default settings. This shows what a new user meets.
2. **Configured-state run.** Configure the app the way the intended user will use it: their vocabulary set, grid size, access method, voice, and any supervisor lock. This shows what a real user lives with.

Record which run each result came from.

Before testing, record:

- Device model and storage free.
- iPadOS or iOS version, including the minor version.
- App name, version, and build number, as shown in the app or in the device's app settings.
- App edition, if the app has more than one (for example, a student or school edition).
- Date and time of testing, and tester names and roles.

### Turning on the platform features

Use the Settings paths below. Paths are written generically; if an OS update moves a setting, search Settings for the feature name. Full paths are in [Appendix B](#appendix-b-settings-paths).

- **VoiceOver:** Settings, then Accessibility, then VoiceOver.
- **Switch Control:** Settings, then Accessibility, then Switch Control. Add switches under Switches before turning Switch Control on.
- **Dynamic Type:** Settings, then Accessibility, then Display and Text Size, then Larger Text. Turn on Larger Accessibility Sizes to reach AX1 to AX5.
- **Reduce Motion:** Settings, then Accessibility, then Motion, then Reduce Motion.
- **Increase Contrast:** Settings, then Accessibility, then Display and Text Size, then Increase Contrast.
- **Guided Access:** Settings, then Accessibility, then Guided Access. Set a passcode. Start a session by triple-clicking the side or Home button inside the app.

Set up the **Accessibility Shortcut** (Settings, then Accessibility, then Accessibility Shortcut) so that triple-clicking the side or Home button toggles the feature under test. This lets the tester switch VoiceOver or Switch Control on and off quickly without leaving the app. Note that if Guided Access is also selected, triple-click shows a menu instead.

### Tester roles

- **Driver:** operates the device using the access method under test. When testing a switch or gaze access method, the driver uses only that method for the steps, never touch, unless the step says otherwise.
- **Observer:** watches, times, and writes observations. Starts and stops screen recordings and names evidence files.
- **Participant (optional):** an AAC user who has given informed consent. The participant is never asked to perform a test that could cause distress, such as repeatedly triggering an emergency phrase in public.

One person can act as driver and observer, but a second person improves the accuracy of timing and announcement records.

### Evidence rules

- Name every evidence file using this convention:

```text
TESTID_app_version_device_os_date.ext

Example:
SC-04_appname_2.3.1_iPad-10th-gen_iPadOS-26.1_2026-10-21.mov
```

- Use hyphens inside each part and underscores between parts. Use the ISO date format (YYYY-MM-DD).
- If one test needs several files, add a sequence suffix before the extension: `_01`, `_02`.
- **Screenshots must show the whole screen**, including the status bar, so the device state (time, network, battery) is visible. Do not crop.
- **Screen recordings must include audio** for any speech output test (SP), any auditory scanning test (SC-06), any VoiceOver announcement test (VO-05, VO-06, VO-08), and any emergency vocabulary speech test (EM-05). Turn on the microphone in the screen recording control if internal audio is not captured, or film the device with a second device.
- **Accessibility Inspector exports** should be saved in the format the tool produces, with the file named by the convention above.
- **Written observations** state what was done, what happened, and what was expected, in plain language.
- Do not capture personal information about a participant in evidence. If a participant's own vocabulary or messages appear on screen, get consent or use a test vocabulary.
- Keep evidence for at least as long as the report is in use, and offer it on request.

### Recording a result

Each test receives exactly one result:

| Result | Definition |
| --- | --- |
| Pass | The test was run on physical hardware as written, and the pass criterion was met. Evidence is recorded. |
| Fail | The test was run on physical hardware as written, and the fail criterion was met, or the pass criterion was not met. Evidence is recorded. |
| Not Applicable | The test does not apply to this app, for a stated reason (for example, the app has no in-app scanner, so SC-04 does not apply). The reason is required. |
| Blocked | The test could not be run, for a stated reason (for example, no eye tracker available, or the app crashed before the step could be reached). A crash that blocks a test should also be reported as a failure under the test where it occurred. |

If a test was not attempted at all, it is reported as Not Evaluated in the report table. Not Evaluated is not a result of a run; it is an honest statement that the test was not done.

### Severity tags

Every Fail receives one severity tag:

| Severity | Definition |
| --- | --- |
| Critical | The failure causes a loss of communication, a safety risk, or a privacy breach. Examples: emergency vocabulary unreachable under the user's access method; the user cannot speak a message; VoiceOver focus is trapped with no way out; message history sent to an undisclosed host. |
| Major | The failure makes a core task much harder or unreliable, but a workaround exists. Examples: scan order differs from visual order; speech cannot be interrupted, but finishes in a few seconds. |
| Minor | The failure causes inconvenience or inconsistency without blocking communication. Examples: a settings label is truncated at AX5 but its meaning is still clear. |

Severity describes impact on the user, not difficulty to fix.

## 4. Test categories

Tests are grouped in twelve categories, in the order of the test ID scheme. Each category begins with why it matters for AAC users and who relies on it, followed by its tests. Every test uses the same seven fields: Setup, Steps, Expected result, Pass criterion, Fail criterion, Evidence to record, and Maps to.

"Every control" in a test means every interactive element on every screen the user can reach during communication, plus the settings screens named in the test. For grid tests, "the grid" means the vocabulary grid in the configured-state run, at the grid size the user will use, plus the densest grid the app offers when a test says so.

## 4.1 VoiceOver (VO)

### Why VoiceOver matters for AAC users

Some AAC users are blind or have low vision, and many have combined vision and motor disabilities, including cortical visual impairment. They navigate the grid by listening. If a symbol cell is announced by its image file name, or not at all, the user cannot find words. If VoiceOver and the app's own speech talk over each other, neither is understood. VoiceOver is also used by partners, teachers, and caregivers who are blind and need to edit or support the user's vocabulary.

### VoiceOver user needs covered

- AAC users who are blind or have low vision and navigate by swiping or touch exploration.
- AAC users with cortical visual impairment who rely on auditory confirmation.
- Communication partners, teachers, and caregivers who use VoiceOver themselves.

### VO-01 Every control has an accessibility label

- **Setup:** Configured-state run. Turn on VoiceOver. Open the main communication screen with a vocabulary set that includes symbol cells, text-only cells, folder or page links, the message bar, and toolbar buttons.
- **Steps:**
  1. Swipe right through every element on the main communication screen, one at a time, from the first element to the last.
  2. For each symbol cell, compare what VoiceOver announces with the word the cell speaks when activated.
  3. Repeat on at least two other vocabulary pages or folders, the message bar, and every toolbar button (speak, clear, delete, back, home, settings).
  4. If a Mac is available, run an Accessibility Inspector audit on the same screens and export the results.
- **Expected result:** Every interactive element has a meaningful label. Each symbol cell's label equals the word or phrase the cell speaks. Icon-only buttons have labels that describe their action.
- **Pass criterion:** Every interactive element on the tested screens is announced with a meaningful label, and every symbol cell's label matches the word the cell speaks.
- **Fail criterion:** Any interactive element is announced with no label, a generic label ("button", "image"), an image file name, an internal identifier, or a label that does not match the spoken word.
- **Evidence to record:** Screen recording with audio of the full swipe-through; list of any unlabeled or mislabeled elements with screenshots; Accessibility Inspector audit export if available.
- **Maps to:** WCAG 2.2 1.1.1 Non-text Content (Level A); WCAG 2.2 4.1.2 Name, Role, Value (Level A); WCAG 2.2 2.4.6 Headings and Labels (Level AA); Apple HIG Accessibility (VoiceOver labels).

### VO-02 Controls expose correct traits

- **Setup:** Configured-state run. Turn on VoiceOver. Have a screen with a selected item (for example, a selected tab or category), a section heading, and any slider or adjustable control (for example, a volume or rate control in settings).
- **Steps:**
  1. Move VoiceOver focus to a symbol cell and note the announced trait.
  2. Move focus to a selected tab, toggle, or category and note whether "selected" is announced.
  3. Move focus to a section or page title and note whether "heading" is announced.
  4. Move focus to a slider or stepper and swipe up and down to adjust it.
- **Expected result:** Cells and buttons announce "button". Selected items announce "selected". Titles announce "heading". Sliders and steppers announce "adjustable" and change value with swipe up and down, with the new value announced.
- **Pass criterion:** Every tested element announces the trait that matches its behavior, and adjustable controls change value with swipe up and down.
- **Fail criterion:** Any actionable element lacks the button trait, selected state is not announced, titles lack the heading trait, or an adjustable control cannot be adjusted with swipe up and down.
- **Evidence to record:** Screen recording with audio; list of elements with missing or wrong traits.
- **Maps to:** WCAG 2.2 4.1.2 Name, Role, Value (Level A); WCAG 2.2 1.3.1 Info and Relationships (Level A); Apple accessibility documentation (accessibility traits).

### VO-03 Focus order follows the reading order of the grid

- **Setup:** Configured-state run. Turn on VoiceOver. Use a grid of at least 4 rows and 4 columns.
- **Steps:**
  1. Place VoiceOver focus on the first element of the screen (four-finger tap near the top, or swipe left until focus stops).
  2. Swipe right through the entire grid, writing down the order of cells announced.
  3. Compare the order with the visual layout.
- **Expected result:** Focus moves through the message bar and toolbar in a logical order, then through the grid row by row, left to right, top to bottom (or right to left for right-to-left languages), without jumping between unrelated regions.
- **Pass criterion:** The announced order matches the visual reading order of the grid, row by row, with no cell skipped or visited twice.
- **Fail criterion:** Focus moves column by column when the grid reads row by row, skips cells, revisits cells, or jumps out of the grid and back in.
- **Evidence to record:** Screen recording with audio; the written announced order beside a screenshot of the grid.
- **Maps to:** WCAG 2.2 2.4.3 Focus Order (Level A); WCAG 2.2 1.3.2 Meaningful Sequence (Level A).

### VO-04 Focus is never trapped and returns sensibly after sheets close

- **Setup:** Configured-state run. Turn on VoiceOver. Identify every sheet, popover, alert, and menu the user can open from the communication screen (for example, a word-forms menu, a settings sheet, a confirmation alert).
- **Steps:**
  1. Open each sheet, popover, alert, or menu with VoiceOver.
  2. Swipe through all of its elements and confirm focus stays inside it while it is open.
  3. Close it using its close or cancel control, and also using the VoiceOver escape gesture (two-finger scrub).
  4. Note where VoiceOver focus lands after it closes.
- **Expected result:** Focus stays inside an open sheet, can always leave it through a labeled control and through the escape gesture, and returns to the control that opened it, or to a logical nearby element.
- **Pass criterion:** Every tested sheet can be closed with VoiceOver, and focus returns to the opening control or a logical nearby element.
- **Fail criterion:** Any sheet cannot be closed with VoiceOver, focus escapes behind an open sheet, or focus lands at an unrelated location (such as the top of the screen) after closing.
- **Evidence to record:** Screen recording with audio for each sheet; list of sheets tested and where focus returned.
- **Maps to:** WCAG 2.2 2.1.2 No Keyboard Trap (Level A); WCAG 2.2 2.4.3 Focus Order (Level A); Apple HIG Accessibility (VoiceOver navigation).

### VO-05 Word additions and spoken messages are announced

- **Setup:** Configured-state run. Turn on VoiceOver. Set the app to add words to the message bar without speaking each word, if that mode exists. Start a screen recording with audio.
- **Steps:**
  1. Activate three symbol cells in a row with VoiceOver (double-tap).
  2. Listen for confirmation after each activation.
  3. Activate the speak control for the whole message.
  4. Move focus to the message bar and listen to its announced content.
- **Expected result:** After each activation, VoiceOver announces the added word or the updated message, or the app speaks the word. When the message is spoken, the user hears the message. Focusing the message bar announces its full current content.
- **Pass criterion:** Each word added to the message bar is confirmed audibly, and focusing the message bar announces the full current message.
- **Fail criterion:** A word is added silently with no audible confirmation, or the message bar announces only a generic label instead of its content.
- **Evidence to record:** Screen recording with audio; written transcript of what was announced after each step.
- **Maps to:** WCAG 2.2 4.1.3 Status Messages (Level AA); WCAG 2.2 4.1.2 Name, Role, Value (Level A).

### VO-06 Page and folder changes are announced

- **Setup:** Configured-state run. Turn on VoiceOver. Use a vocabulary set with at least two levels of folders or pages.
- **Steps:**
  1. Activate a folder or page link with VoiceOver.
  2. Listen to what is announced when the new page appears.
  3. Use the app's back or home control and listen again.
  4. Note where focus lands on each new page.
- **Expected result:** On each page change, VoiceOver announces the new page or folder name (or the screen change sound plays and focus moves to the page title or first cell), so the user knows where they are.
- **Pass criterion:** Every page or folder change produces an audible indication of the new page name, and focus moves to a predictable element on the new page.
- **Fail criterion:** The page changes silently with focus left on a cell that no longer exists or on an unrelated element, or the user cannot tell which page is showing.
- **Evidence to record:** Screen recording with audio of at least three page changes.
- **Maps to:** WCAG 2.2 4.1.3 Status Messages (Level AA); WCAG 2.2 2.4.2 Page Titled (Level A); WCAG 2.2 3.2.1 On Focus (Level A).

### VO-07 Custom actions do not hide essential functions

- **Setup:** Configured-state run. Turn on VoiceOver. Identify any functions available on a cell by long press, swipe, or context menu (for example, word forms, plurals, edit, hide).
- **Steps:**
  1. Focus a cell that has extra functions and swipe up or down to hear the custom actions VoiceOver offers.
  2. Check that every function available to touch users through long press or gesture is available to VoiceOver users, either as a custom action or as a visible control.
  3. Check that essential communication functions (speak, delete last word, clear, go home) are available as visible, focusable controls, not only as custom actions.
- **Expected result:** Every gesture-based function has a VoiceOver equivalent. Essential communication functions are standalone controls that can be found by swiping, not only buried in custom actions.
- **Pass criterion:** All gesture-only functions are reachable with VoiceOver, and speak, delete, clear, and home are each reachable as a standalone focusable control.
- **Fail criterion:** Any function is reachable only by a gesture VoiceOver users cannot perform, or an essential communication function is reachable only through a custom action.
- **Evidence to record:** Screen recording with audio; list of gesture functions and their VoiceOver equivalents.
- **Maps to:** WCAG 2.2 2.5.1 Pointer Gestures (Level A); WCAG 2.2 2.1.1 Keyboard (Level A); Apple accessibility documentation (accessibility custom actions).

### VO-08 VoiceOver and app speech do not conflict

- **Setup:** Configured-state run. Turn on VoiceOver. Set the app to speak each word on selection, if that mode exists. Start a screen recording with audio.
- **Steps:**
  1. Activate a symbol cell with VoiceOver and listen.
  2. Activate the speak control with a message of at least five words and listen.
  3. While the message is speaking, swipe to the next element.
  4. Check the app's documentation or settings for a description of how its speech and VoiceOver interact.
- **Expected result:** Both VoiceOver and the app's speech are audible and understandable. Either the app's speech waits for VoiceOver to finish, VoiceOver is not cut off mid-word, or the app documents a setting that controls the behavior. The user's message is never lost or truncated because of VoiceOver.
- **Pass criterion:** The full message is audible and intelligible with VoiceOver on, and VoiceOver announcements are not lost, or the app's documented behavior is followed exactly.
- **Fail criterion:** The app's speech and VoiceOver speak at the same time so that either is unintelligible, the message is cut off, or VoiceOver silences the app's speech with no documented setting.
- **Evidence to record:** Screen recording with audio; quote or screenshot of any documentation describing the behavior.
- **Maps to:** Revised Section 508 502.2.2 No Disruption of Accessibility Features; WCAG 2.2 1.4.2 Audio Control (Level A); Apple accessibility documentation (posting announcements and speech).

### VO-09 Rotor and heading navigation work

- **Setup:** Configured-state run. Turn on VoiceOver. Open the main communication screen and one settings screen.
- **Steps:**
  1. Open the VoiceOver rotor (two-finger rotate) and select Headings.
  2. Swipe down and up to move between headings.
  3. On the communication screen, check whether regions (message bar, toolbar, grid, page navigation) can be reached by heading or by a rotor option.
  4. On the settings screen, check that section titles are headings.
- **Expected result:** Major regions and settings sections are marked as headings or are otherwise reachable through the rotor, so the user can jump between regions without swiping through every cell.
- **Pass criterion:** The rotor's Headings option moves between the major regions of the communication screen and between the sections of the settings screen.
- **Fail criterion:** No headings are exposed, or the user must swipe through every cell to reach the message bar or toolbar from the bottom of the grid.
- **Evidence to record:** Screen recording with audio; list of headings announced.
- **Maps to:** WCAG 2.2 2.4.1 Bypass Blocks (Level A); WCAG 2.2 1.3.1 Info and Relationships (Level A); WCAG 2.2 2.4.6 Headings and Labels (Level AA).

### VO-10 Decorative images are hidden from VoiceOver

- **Setup:** Configured-state run. Turn on VoiceOver. Identify decorative elements: background art, mascots, borders, dividers, and symbol images inside cells that already have a label.
- **Steps:**
  1. Swipe through the main communication screen and the home or start screen.
  2. Note any element that receives focus but has no function and conveys no information.
  3. Check that a symbol cell is a single focusable element, not a separate image and label that each receive focus.
- **Expected result:** Decorative elements are skipped by VoiceOver. Each cell is announced once as a single element.
- **Pass criterion:** No purely decorative element receives VoiceOver focus, and each cell is one focusable element.
- **Fail criterion:** Any decorative element receives focus, or a cell's image and text are announced as separate elements.
- **Evidence to record:** Screen recording with audio; list of decorative elements that received focus.
- **Maps to:** WCAG 2.2 1.1.1 Non-text Content (Level A); WCAG 2.2 1.3.1 Info and Relationships (Level A).

## 4.2 Switch Control and in-app scanning (SC)

### Why switch access matters for AAC users

Many AAC users have significant motor disabilities and communicate with one or two switches. They depend on scanning: the system highlights items one at a time or in groups, and the user activates a switch to choose. Scanning is slow by nature, so every unnecessary step, every skipped item, and every accidental double activation costs real communication time and causes real frustration. A scan that cannot reach the speak button or the emergency area silences the user. AAC apps can be used with iPadOS Switch Control, with the app's own built-in scanner, or both, and both paths must work.

### Switch access user needs covered

- AAC users with physical disabilities who use one switch (auto scan) or two switches (step scan).
- AAC users who are blind or have low vision and use auditory scanning.
- AAC users with fatigue or variable motor control who need adjustable timing and debounce.

### SC-01 iPadOS Switch Control reaches every interactive element

- **Setup:** Configured-state run. Connect a switch interface and a switch. In Settings, add the switch for Select Item and turn on Switch Control with auto scanning. Turn off the app's own scanner, if it has one.
- **Steps:**
  1. Open the communication screen and let Switch Control scan the whole screen.
  2. Using only the switch, try to reach and activate every cell on the grid, the speak control, delete, clear, home, back, page navigation, and the settings entry point.
  3. Open a folder and a sheet using only the switch, and close them.
- **Expected result:** Switch Control can highlight and activate every interactive element, including those inside sheets and menus.
- **Pass criterion:** Every interactive element on the tested screens can be reached and activated using only the switch with iPadOS Switch Control.
- **Fail criterion:** Any interactive element is never highlighted or cannot be activated with Switch Control.
- **Evidence to record:** Screen recording of the scan; list of elements not reached.
- **Maps to:** WCAG 2.2 2.1.1 Keyboard (Level A); WCAG 2.2 4.1.2 Name, Role, Value (Level A); Revised Section 508 502.3 Accessibility Services; Apple HIG Accessibility (Switch Control).

### SC-02 Scan order matches visual order

- **Setup:** Configured-state run. Use the app's own scanner if it has one; otherwise use iPadOS Switch Control. Use a grid of at least 4 rows and 4 columns.
- **Steps:**
  1. Start scanning from the top of the screen.
  2. Record the order in which regions and items are highlighted.
  3. Compare it with the visual layout of the screen.
- **Expected result:** Regions are scanned in a consistent, logical order (for example, message bar, toolbar, grid), and items within the grid are scanned in reading order.
- **Pass criterion:** The scan order follows the visual reading order of the screen, with no item skipped and no item highlighted out of sequence.
- **Fail criterion:** The scan order jumps between unrelated regions, skips items, or scans the grid in an order that does not match its visual layout.
- **Evidence to record:** Screen recording; written scan order beside a screenshot.
- **Maps to:** WCAG 2.2 2.4.3 Focus Order (Level A); WCAG 2.2 1.3.2 Meaningful Sequence (Level A).

### SC-03 Group and item scanning works on the grid

- **Setup:** Configured-state run. Use the app's own scanner set to row-column (or group-item) scanning if available; otherwise use iPadOS Switch Control with Group Items turned on.
- **Steps:**
  1. Start scanning. Confirm that rows (or groups) are highlighted first.
  2. Activate the switch on a row, then confirm items within that row are highlighted one at a time.
  3. Select a cell in the last row, last column.
  4. Let a row scan finish without a selection and note what happens.
- **Expected result:** Group scanning narrows to the chosen row or group, then scans its items. If the user does not select an item, the scanner returns to group scanning after a set number of cycles, rather than looping inside the row forever.
- **Pass criterion:** The user can select any cell, including the last cell of the last row, by group-then-item scanning, and an unselected row returns to group level after a defined number of loops.
- **Fail criterion:** Group scanning is unavailable for the grid, any cell cannot be reached, or the scanner loops inside a row with no way back to group level except by selecting an item.
- **Evidence to record:** Screen recording; note of the number of loops before return to group level.
- **Maps to:** WCAG 2.2 2.1.1 Keyboard (Level A); WCAG 2.2 2.2.1 Timing Adjustable (Level A).

### SC-04 In-app auto-scan timing is adjustable across its full range

- **Setup:** Configured-state run with the app's own scanner. If the app has no scanner of its own, record Not Applicable and rely on SC-01 and the iPadOS Switch Control timing settings. Connect one switch.
- **Steps:**
  1. Open the app's scan settings and record the minimum and maximum scan rate (time each item is highlighted) and the step size.
  2. Set the scan rate to the minimum. Scan one full cycle of the grid and time three items with a stopwatch or from the recording.
  3. Set the scan rate to the maximum and repeat.
  4. Set a middle value and confirm the setting persists after the app is closed and reopened.
- **Expected result:** The scan rate is adjustable across a documented range that includes at least 0.5 seconds to 5 seconds per item, the measured highlight duration matches the setting within about 10 percent, and the setting persists.
- **Pass criterion:** The scan rate range includes at least 0.5 to 5 seconds per item, the measured timing at the minimum and maximum matches the settings within 10 percent, and the setting persists after relaunch.
- **Fail criterion:** The range is narrower than 0.5 to 5 seconds, the measured timing differs from the setting by more than 10 percent, or the setting resets after relaunch.
- **Evidence to record:** Screenshot of scan settings at minimum and maximum; screen recording at each setting; measured timings.
- **Maps to:** WCAG 2.2 2.2.1 Timing Adjustable (Level A); Revised Section 508 503.2 User Preferences.

### SC-05 Scanning can be paused, and the user can hold or skip

- **Setup:** Configured-state run with the app's own scanner, or with iPadOS Switch Control. One or two switches connected.
- **Steps:**
  1. During auto scan, use the documented pause method (for example, a pause switch, a pause item in the scan, or the Switch Control menu) and confirm scanning stops.
  2. Wait at least 30 seconds and confirm scanning stays paused and the message is kept.
  3. Resume scanning.
  4. If the app offers hold-to-skip or a "move to next group" action, test it.
- **Expected result:** The user can pause scanning without selecting anything, the message bar content is kept while paused, and scanning resumes from a predictable point.
- **Pass criterion:** Scanning can be paused and resumed by the switch user without touch, and the message is unchanged after a 30 second pause.
- **Fail criterion:** Scanning cannot be paused by the switch user, the pause requires touch, or the message is lost or changed during the pause.
- **Evidence to record:** Screen recording including the pause and resume.
- **Maps to:** WCAG 2.2 2.2.2 Pause, Stop, Hide (Level A); WCAG 2.2 2.2.1 Timing Adjustable (Level A).

### SC-06 Auditory scanning uses a separate cue channel with its own volume

- **Setup:** Configured-state run with the app's own scanner, if the app offers auditory scanning. If it does not, record Not Applicable and note that auditory scanning is not offered. Connect headphones and confirm whether the app can route cues and message speech to different outputs.
- **Steps:**
  1. Turn on auditory scanning. Start auto scan and listen to the cue for each item.
  2. Select three words and speak the message.
  3. Compare the cue voice or sound with the message voice.
  4. Adjust the cue volume and the message volume separately, if the app offers separate controls.
  5. If the app supports routing cues to headphones and the message to the speaker, test it.
- **Expected result:** Each scanned item is cued audibly (for example, a quieter or different voice, or a short prompt word). The cue is clearly distinct from the message voice, so a listener can tell the user is browsing rather than speaking. Cue volume is adjustable independently.
- **Pass criterion:** Every scanned item produces an audible cue that is distinguishable from the message voice, and the cue volume can be set independently of the message volume.
- **Fail criterion:** Any item is not cued, the cue uses the same voice and volume as the message with no option to change it, or cue volume cannot be adjusted separately.
- **Evidence to record:** Screen recording with audio; screenshots of auditory scanning settings.
- **Maps to:** WCAG 2.2 1.4.2 Audio Control (Level A); Revised Section 508 302.1 Without Vision; Revised Section 508 503.2 User Preferences.

### SC-07 The visual scan highlight is visible in every display mode

- **Setup:** Configured-state run with the app's own scanner, and separately with iPadOS Switch Control. Capture screenshots of the highlight in light mode, dark mode, with Increase Contrast on, and with Smart Invert on.
- **Steps:**
  1. Capture a screenshot with the scan highlight on a cell in each display mode.
  2. Measure the highlight's contrast against the cell and the surrounding background with a contrast tool.
  3. Check the app's scan highlight settings for color and thickness options.
  4. Ask a tester with low vision, if available, to locate the highlight from normal viewing distance.
- **Expected result:** The highlight has at least 3:1 contrast against adjacent colors in every display mode, is at least as thick as the cell border, and its color and thickness can be changed in the app's own scanner.
- **Pass criterion:** The highlight has at least 3:1 contrast against adjacent colors in all four display modes, and the app's own scanner offers at least one way to make the highlight thicker or change its color.
- **Fail criterion:** The highlight falls below 3:1 contrast in any display mode, disappears against any cell color, or cannot be adjusted in the app's own scanner.
- **Evidence to record:** Screenshots in each mode with measured contrast ratios; screenshot of highlight settings.
- **Maps to:** WCAG 2.2 1.4.11 Non-text Contrast (Level AA); WCAG 2.2 2.4.7 Focus Visible (Level AA); WCAG 2.2 2.4.13 Focus Appearance (Level AAA).

### SC-08 One-switch auto scan and two-switch step scan both work

- **Setup:** Configured-state run. Connect two switches. Configure one-switch auto scan first, then two-switch step scan (one switch moves, one switch selects), using the app's scanner or iPadOS Switch Control.
- **Steps:**
  1. With one-switch auto scan, build and speak a three-word message.
  2. Switch to two-switch step scan. Confirm the move switch advances one item per press and the select switch selects.
  3. Build and speak a three-word message with step scan.
  4. Confirm that in step scan the highlight does not advance on its own.
- **Expected result:** Both modes allow building and speaking a full message. In step scan, the highlight moves only on a switch press.
- **Pass criterion:** A three-word message can be built and spoken in both one-switch auto scan and two-switch step scan, and step scan never advances without a press.
- **Fail criterion:** Either mode is unavailable through both the app's scanner and iPadOS Switch Control, a message cannot be completed in either mode, or step scan advances automatically.
- **Evidence to record:** Screen recording of both modes; screenshot of switch configuration.
- **Maps to:** WCAG 2.2 2.1.1 Keyboard (Level A); WCAG 2.2 2.2.1 Timing Adjustable (Level A).

### SC-09 Switch acceptance time and debounce prevent double activation

- **Setup:** Configured-state run with the app's own scanner if it has acceptance and debounce settings, and with iPadOS Switch Control (Hold Duration and Ignore Repeat settings). One switch connected.
- **Steps:**
  1. Set a hold or acceptance time (for example, 0.3 seconds). Tap the switch briefly (shorter than the acceptance time) and confirm nothing is selected. Hold it longer and confirm a selection.
  2. Set a debounce or ignore-repeat time (for example, 0.5 seconds). Press the switch twice in quick succession within that window and confirm only one selection is made.
  3. With debounce off, press quickly twice and record what happens, for comparison.
- **Expected result:** Presses shorter than the acceptance time are ignored, repeated presses within the debounce window produce a single selection, and no word is added twice by a single intended press.
- **Pass criterion:** With acceptance and debounce set, short presses are ignored and rapid repeated presses produce exactly one selection.
- **Fail criterion:** A press shorter than the acceptance time selects an item, or a rapid double press within the debounce window adds a word twice or selects two items.
- **Evidence to record:** Screen recording with the switch visible, or a second camera filming the switch; screenshots of the settings used.
- **Maps to:** WCAG 2.2 2.5.2 Pointer Cancellation (Level A); EN 301 549 5.8 Double-strike key acceptance; Apple HIG Accessibility (Switch Control).

### SC-10 Scanning never loses the message bar or the emergency area

- **Setup:** Configured-state run with the app's own scanner and with iPadOS Switch Control. Use a vocabulary with at least two levels of folders and an emergency or help area.
- **Steps:**
  1. Navigate two levels deep into folders using only the switch.
  2. Confirm the scan still includes the message bar (or speak control) and the emergency area on that page, or a single scan step that reaches them.
  3. Open any sheet or menu and confirm the scan can leave it to reach the message bar.
- **Expected result:** On every page, the switch user can reach the speak control and the emergency area within one scan cycle.
- **Pass criterion:** On every tested page, the speak control and the emergency area are reachable within one full scan cycle using only the switch.
- **Fail criterion:** On any page, the speak control or emergency area is not included in the scan, or the user must back out through several levels to reach them.
- **Evidence to record:** Screen recording showing one full scan cycle on each tested page.
- **Maps to:** WCAG 2.2 3.2.3 Consistent Navigation (Level AA); WCAG 2.2 3.2.6 Consistent Help (Level A); WCAG 2.2 2.1.1 Keyboard (Level A).

### SC-11 Scanning restarts predictably after a selection

- **Setup:** Configured-state run with the app's own scanner. Note the scanner's documented restart behavior (for example, restart at the top, or continue from the selected item).
- **Steps:**
  1. Select a cell in the middle of the grid.
  2. Note where scanning restarts.
  3. Select a folder link and note where scanning starts on the new page.
  4. Repeat each step three times.
- **Expected result:** After every selection, scanning restarts from the same documented position each time. After a page change, scanning starts at a consistent position on the new page.
- **Pass criterion:** In all repetitions, scanning restarts from the same position after a cell selection and from the same position after a page change, consistent with the app's documented behavior or setting.
- **Fail criterion:** The restart position varies between repetitions, or differs from the documented behavior.
- **Evidence to record:** Screen recording of all repetitions; quote or screenshot of the documented behavior.
- **Maps to:** WCAG 2.2 3.2.1 On Focus (Level A); WCAG 2.2 3.2.3 Consistent Navigation (Level AA).

### SC-12 In-app scanning does not conflict with iPadOS Switch Control

- **Setup:** Configured-state run. The app has its own scanner. Connect a switch.
- **Steps:**
  1. Read the app's documentation for guidance on whether to use its own scanner or iPadOS Switch Control.
  2. Turn on both the app's scanner and iPadOS Switch Control at the same time and press the switch.
  3. Turn off iPadOS Switch Control and confirm the app's scanner works alone.
  4. Turn off the app's scanner, turn on iPadOS Switch Control, and confirm it works alone.
- **Expected result:** The app documents which scanner to use and how they interact. When both are on, the app either detects the conflict and warns, or behaves in the documented way. A single switch press never produces two different actions.
- **Pass criterion:** The app documents how its scanner and iPadOS Switch Control interact, and when both are on, a switch press produces only one action.
- **Fail criterion:** No documentation exists, or a single switch press triggers both scanners, producing two actions or an unusable state.
- **Evidence to record:** Screen recording with both on; quote or screenshot of documentation.
- **Maps to:** Revised Section 508 502.2.2 No Disruption of Accessibility Features; WCAG 2.2 4.1.2 Name, Role, Value (Level A).

## 4.3 Eye gaze and dwell (EG)

### Why eye gaze matters for AAC users

Some AAC users have very limited movement and communicate with their eyes. An eye tracker moves a pointer to where the user looks, and holding the gaze on a target for a set time (dwell) selects it. Eyes are for looking as well as selecting, so gaze access has a unique problem: anything the user looks at long enough may be selected, including the message they are trying to read. Eye gaze users also tire quickly and need rest. Targets must be larger than for touch, because gaze tracking is less precise than a fingertip and drifts over time.

### Eye gaze user needs covered

- AAC users with severe motor disabilities who use an eye tracker with dwell selection.
- AAC users who use a head pointer or other external pointing device with dwell, through AssistiveTouch.
- Users who tire quickly and need rest areas and adjustable dwell times.

### EG-01 An eye tracker works through the platform pointer path or the app's own gaze mode

- **Setup:** Fresh install run, then configured-state run. Connect a USB or Bluetooth eye tracker supported by the device, or an external pointing device. Turn on AssistiveTouch and its dwell control, or the app's own gaze mode if it has one.
- **Steps:**
  1. Read the app's documentation for its supported eye gaze path (platform AssistiveTouch dwell, the app's own gaze mode, or both).
  2. Using only gaze and dwell, build and speak a three-word message.
  3. Using only gaze and dwell, navigate into a folder and back.
- **Expected result:** The app works with gaze and dwell through at least one documented path, and a full message can be built and spoken.
- **Pass criterion:** A three-word message can be built and spoken, and a folder entered and exited, using only gaze and dwell through a documented path.
- **Fail criterion:** No documented gaze path exists, or the message or navigation cannot be completed with gaze and dwell alone.
- **Evidence to record:** Screen recording; a second camera recording of the user's or tester's eyes and the screen if possible; quote or screenshot of documentation.
- **Maps to:** WCAG 2.2 2.5.1 Pointer Gestures (Level A); Revised Section 508 302.7 With Limited Manipulation; Apple HIG Accessibility (AssistiveTouch and pointer support).

### EG-02 Calibration is reachable without gaze

- **Setup:** Configured-state run with gaze active. Ask the tester to imagine calibration has drifted so gaze selection is unreliable.
- **Steps:**
  1. Locate the calibration control for the gaze path in use (platform or app).
  2. Confirm a caregiver can start calibration by touch, from a location that does not require gaze.
  3. Confirm the calibration process itself can be completed by the gaze user without needing to select small targets.
- **Expected result:** A caregiver can start recalibration by touch within two actions from the communication screen or from a documented system location, and calibration uses large, clearly shown targets.
- **Pass criterion:** Calibration can be started by touch without using gaze, from a documented location, and completed by the gaze user.
- **Fail criterion:** Starting calibration requires accurate gaze selection, or calibration cannot be found or completed.
- **Evidence to record:** Screen recording of starting and completing calibration; note of the location of the control.
- **Maps to:** WCAG 2.2 3.3.2 Labels or Instructions (Level A); WCAG 2.2 2.5.1 Pointer Gestures (Level A).

### EG-03 Gaze targets are large enough and spaced apart

- **Setup:** Configured-state run with the grid size the gaze user will use. Take a full-screen screenshot.
- **Steps:**
  1. Measure the width and height of the smallest gaze-selectable cell in points, using the method in the Touch targets category (TT measurement method).
  2. Measure the gutter (empty, non-selectable space) between adjacent cells.
  3. Repeat for toolbar buttons and the speak control in gaze mode.
- **Expected result:** This protocol recommends an effective gaze target of at least 60 x 60 points, with a non-selectable gutter between cells. Gaze trackers have lower accuracy than touch and drift over a session, so a target that is fine for a fingertip can be unreliable for gaze. Gutters reduce selection of a neighboring cell when the gaze point drifts.
- **Pass criterion:** Every gaze-selectable target on the tested screen is at least 60 x 60 points, with a visible gutter between adjacent cells, or the app offers a gaze layout that meets this.
- **Fail criterion:** Any gaze-selectable target is smaller than 60 x 60 points in every available gaze layout, or adjacent cells have no gutter.
- **Evidence to record:** Annotated screenshot with measurements; device model and its point scale.
- **Maps to:** WCAG 2.2 2.5.5 Target Size (Enhanced) (Level AAA); WCAG 2.2 2.5.8 Target Size (Minimum) (Level AA).

### EG-04 Dwell time is adjustable across a stated range

- **Setup:** Configured-state run with gaze active.
- **Steps:**
  1. Open dwell settings (platform AssistiveTouch dwell or the app's gaze settings) and record the minimum and maximum dwell time.
  2. Set the minimum and select three cells, timing the dwell from the recording.
  3. Set the maximum and repeat.
  4. Confirm the setting persists after the app is closed and reopened.
- **Expected result:** Dwell time is adjustable across a documented range that includes at least 0.5 seconds to 3 seconds, the measured dwell matches the setting, and it persists.
- **Pass criterion:** Dwell time can be set across a range that includes at least 0.5 to 3 seconds, the measured dwell matches the setting within 10 percent, and the setting persists after relaunch.
- **Fail criterion:** The dwell range is narrower than 0.5 to 3 seconds, the measured dwell differs by more than 10 percent, or the setting resets.
- **Evidence to record:** Screenshots of settings at minimum and maximum; screen recording with measured times.
- **Maps to:** WCAG 2.2 2.2.1 Timing Adjustable (Level A); Revised Section 508 503.2 User Preferences.

### EG-05 Dwell progress feedback is visible

- **Setup:** Configured-state run with gaze active, in light mode and dark mode.
- **Steps:**
  1. Dwell on a cell and observe the feedback during the dwell (for example, a filling ring, shrinking dot, or changing border).
  2. Look away halfway through and observe whether the feedback resets.
  3. Measure the feedback's contrast against the cell in both modes.
- **Expected result:** A visible progress indicator shows dwell progress, resets when gaze leaves the target, and has at least 3:1 contrast against the cell.
- **Pass criterion:** A dwell progress indicator is shown on every gaze-selectable target, resets when gaze leaves, and has at least 3:1 contrast in light and dark mode.
- **Fail criterion:** No progress indicator is shown, it does not reset when gaze leaves, or its contrast is below 3:1 in either mode.
- **Evidence to record:** Screen recording; screenshots mid-dwell in both modes with contrast measurements.
- **Maps to:** WCAG 2.2 1.4.11 Non-text Contrast (Level AA); WCAG 2.2 2.4.7 Focus Visible (Level AA).

### EG-06 Resting gaze and reading the message do not cause selections

- **Setup:** Configured-state run with gaze active and dwell at a typical setting (for example, 1 second). Build a message of at least six words.
- **Steps:**
  1. Read the message in the message bar with the eyes for 10 seconds.
  2. Look at the page title, decorative areas, and any blank space for 10 seconds each.
  3. Note whether any selection occurs.
- **Expected result:** The message bar, titles, and decorative areas are not dwell targets, or they require a distinctly longer dwell, or the message bar has a separate, clearly labeled speak target. Reading the message does not speak it, clear it, or change it.
- **Pass criterion:** No selection occurs while reading the message bar or looking at non-interactive areas for 10 seconds each at the tested dwell setting.
- **Fail criterion:** Any selection, speech, clearing, or message change occurs while reading the message bar or looking at non-interactive areas.
- **Evidence to record:** Screen recording with eye-position overlay if the gaze path shows one.
- **Maps to:** WCAG 2.2 3.2.1 On Focus (Level A); WCAG 2.2 2.5.2 Pointer Cancellation (Level A).

### EG-07 A rest or pause area exists for gaze users

- **Setup:** Configured-state run with gaze active.
- **Steps:**
  1. Locate a rest area, pause control, or gaze-off toggle reachable by gaze.
  2. Activate it with gaze and rest the gaze anywhere on the screen for 30 seconds.
  3. Resume gaze selection with gaze alone.
- **Expected result:** The gaze user can pause selection with gaze, look anywhere on screen without selecting, and resume with gaze, without caregiver help.
- **Pass criterion:** The gaze user can pause and resume selection using gaze alone, and no selection occurs during a 30 second pause.
- **Fail criterion:** No pause exists, pausing or resuming needs touch, or a selection occurs during the pause.
- **Evidence to record:** Screen recording of pause, rest, and resume.
- **Maps to:** WCAG 2.2 2.2.2 Pause, Stop, Hide (Level A); WCAG 2.2 2.1.1 Keyboard (Level A).

### EG-08 Recovery from tracker disconnect keeps the message

- **Setup:** Configured-state run with gaze active. Build a message of at least three words.
- **Steps:**
  1. Disconnect the eye tracker (unplug it, or turn off its Bluetooth connection).
  2. Observe the app for 30 seconds.
  3. Reconnect the tracker and resume gaze selection.
  4. Speak the message.
- **Expected result:** The app does not crash or clear the message on disconnect. It shows or speaks a notice that the tracker is disconnected, if it can detect it. After reconnecting, gaze selection resumes and the message is intact.
- **Pass criterion:** After disconnecting and reconnecting the tracker, the message is intact and can be spoken, and gaze selection resumes without restarting the app.
- **Fail criterion:** The app crashes, clears or changes the message, or requires a restart to resume gaze selection.
- **Evidence to record:** Screen recording through disconnect and reconnect.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA); Revised Section 508 302.7 With Limited Manipulation.

## 4.4 Touch targets (TT)

### Why touch target size matters for AAC users

Many AAC users who touch the screen directly have motor disabilities such as cerebral palsy, tremor, or reduced range of motion. Small targets cause missed words and wrong words. A wrong word in an AAC message is not a typo: it changes what the person said. Large, well-spaced targets and support for platform touch accommodations are basic requirements.

### Touch target user needs covered

- AAC users who use direct touch with limited fine motor control, tremor, or spasticity.
- AAC users who use a keyguard over the screen.
- Users who rely on platform Touch Accommodations (Hold Duration, Ignore Repeat, Tap Assistance).

### TT measurement method

Use one of these methods to measure target size in points (pt), the device-independent unit used by iPadOS and iOS:

- **Accessibility Inspector:** connect the device to a Mac, open Accessibility Inspector, select the device, and point at an element. The inspector reports the element's frame in points.
- **Screenshot overlay:** take a full-screen screenshot. Find the device's screen scale factor (2x or 3x for current devices) in the device's published specifications. Divide the pixel width and height of a target in the screenshot by the scale factor to get points. Measure the tappable area if it is visible (for example, a cell background), not just the icon.

Record the method used, the device model, and the scale factor with every measurement.

### TT-01 Every interactive element is at least 44 x 44 points

- **Setup:** Configured-state run at the grid size the user will use. Measure using the TT measurement method.
- **Steps:**
  1. Measure every grid cell size (cells in a uniform grid can be measured once per size).
  2. Measure every toolbar button, the speak control, delete, clear, home, back, page navigation, and the message bar's controls.
  3. Measure controls on any sheet the user opens during communication.
- **Expected result:** Every interactive element is at least 44 x 44 points. WCAG 2.5.8 Target Size (Minimum) at Level AA requires 24 x 24 CSS pixels, and the Apple HIG recommends 44 x 44 points. This protocol requires 44 x 44 points for AAC apps, because mis-selection changes what the user says. Grid cells for users with significant motor disabilities usually need to be much larger than 44 points, and the app should offer larger cell sizes.
- **Pass criterion:** Every measured interactive element used during communication is at least 44 x 44 points.
- **Fail criterion:** Any interactive element used during communication is smaller than 44 x 44 points.
- **Evidence to record:** Annotated screenshots with measurements; Accessibility Inspector frames if used; device scale factor.
- **Maps to:** WCAG 2.2 2.5.8 Target Size (Minimum) (Level AA); WCAG 2.2 2.5.5 Target Size (Enhanced) (Level AAA); Apple HIG Accessibility (minimum hit target 44 x 44 pt).

### TT-02 Adjacent cells are spaced to prevent mis-selection

- **Setup:** Configured-state run at the grid size the user will use.
- **Steps:**
  1. Measure the gap between adjacent cells horizontally and vertically.
  2. Tap the exact boundary between two cells ten times and note which cell, if any, activates.
  3. Check settings for a cell spacing or gutter option.
- **Expected result:** Cells have visible spacing between them, a tap on the boundary activates at most one cell, and spacing is adjustable or sufficient by default.
- **Pass criterion:** Adjacent cells have a visible gap, and no boundary tap activates two cells.
- **Fail criterion:** Cells touch with no gap and no spacing option exists, or a single boundary tap activates two cells.
- **Evidence to record:** Annotated screenshot with gap measurements; screen recording of boundary taps.
- **Maps to:** WCAG 2.2 2.5.8 Target Size (Minimum) (Level AA).

### TT-03 The densest grid still meets the minimum or the app warns

- **Setup:** Configured-state run. Set the grid to the largest number of rows and columns the app offers, on the smallest supported screen being tested (for example, iPhone if supported).
- **Steps:**
  1. Measure the cell size at the densest grid setting.
  2. If cells are smaller than 44 x 44 points, check whether the app shows a warning or explanation when choosing that density.
- **Expected result:** At every grid density, cells are at least 44 x 44 points, or the app clearly warns that the chosen density produces targets below the recommended minimum.
- **Pass criterion:** At the densest grid setting, cells are at least 44 x 44 points, or a warning is shown when that density is chosen.
- **Fail criterion:** Cells are smaller than 44 x 44 points at the densest setting and no warning is shown.
- **Evidence to record:** Screenshot at densest grid with measurements; screenshot of any warning.
- **Maps to:** WCAG 2.2 2.5.8 Target Size (Minimum) (Level AA); WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA).

### TT-04 Platform Touch Accommodations work with the app

- **Setup:** Configured-state run. In Settings, turn on Touch Accommodations, set Hold Duration (for example, 0.5 seconds), Ignore Repeat (for example, 1 second), and Tap Assistance (use initial or final touch location).
- **Steps:**
  1. With Hold Duration on, tap a cell briefly and confirm nothing is selected, then hold it and confirm selection.
  2. With Ignore Repeat on, tap a cell twice quickly and confirm one word is added.
  3. With Tap Assistance on, touch one cell and drag to another before lifting, and confirm the documented location rule is followed.
  4. Check whether the app has its own activation settings (for example, select on release, or ignore drags) and confirm they do not conflict with the platform settings.
- **Expected result:** Each Touch Accommodation behaves as documented by the platform inside the app. The app's own touch settings, if any, work together with the platform settings.
- **Pass criterion:** Hold Duration, Ignore Repeat, and Tap Assistance each behave as documented inside the app's communication screen.
- **Fail criterion:** Any Touch Accommodation is ignored or behaves differently inside the app, or the app's own touch settings cause double or missed selections when combined with the platform settings.
- **Evidence to record:** Screen recording with a second camera on the tester's hand if possible; screenshots of settings.
- **Maps to:** WCAG 2.2 2.5.2 Pointer Cancellation (Level A); Revised Section 508 502.2.2 No Disruption of Accessibility Features; Revised Section 508 302.7 With Limited Manipulation.

### TT-05 Dragging and multi-finger gestures have single-tap alternatives

- **Setup:** Configured-state run. List every action that uses a drag, swipe, pinch, or multi-finger gesture (for example, swiping between pages, dragging to reorder cells, pinching to resize).
- **Steps:**
  1. For each gesture-based action, look for an equivalent that uses single taps.
  2. Perform the action using only single taps.
- **Expected result:** Every action that uses a drag or multi-finger gesture can also be done with single taps, for example page arrows in place of swiping.
- **Pass criterion:** Every gesture-based action has a single-tap alternative.
- **Fail criterion:** Any action, including page navigation, requires a drag, swipe, or multi-finger gesture with no single-tap alternative.
- **Evidence to record:** List of gesture actions and their alternatives; screen recording.
- **Maps to:** WCAG 2.2 2.5.7 Dragging Movements (Level AA); WCAG 2.2 2.5.1 Pointer Gestures (Level A).

## 4.5 Dynamic Type (DT)

### Why Dynamic Type matters for AAC users

AAC users, partners, and caregivers may have low vision. Text in cells and the message bar must grow when the person needs it to, and must still fit. A word cut off to "beauti..." or a message bar that hides the last word is a communication failure. Caregivers with low vision also need to read settings to support the user.

### Dynamic Type user needs covered

- AAC users with low vision who read cell labels and the message bar.
- Communication partners and caregivers with low vision.
- Users who set a larger default text size across all apps.

### DT-01 Text scales at accessibility sizes AX1 to AX5

- **Setup:** Configured-state run. In Settings, turn on Larger Accessibility Sizes.
- **Steps:**
  1. Set text size to the default and capture a screenshot of the communication screen.
  2. Set text size to AX1, AX3, and AX5 in turn, returning to the app each time, and capture screenshots.
  3. Compare the size of cell labels, message bar text, and toolbar labels across screenshots.
- **Expected result:** Cell labels, message bar text, and toolbar text grow as the text size increases, up to AX5, or the app documents a fixed-size design for cell labels along with its own size control (see DT-04).
- **Pass criterion:** Message bar and toolbar text grow at each step from default to AX5, and cell labels grow or are controlled by a documented in-app size setting.
- **Fail criterion:** Message bar or toolbar text does not change with Dynamic Type, or cell labels neither scale nor have an in-app size control.
- **Evidence to record:** Screenshots at default, AX1, AX3, and AX5.
- **Maps to:** WCAG 2.2 1.4.4 Resize Text (Level AA); Apple HIG Accessibility (Dynamic Type).

### DT-02 No words are truncated or clipped at AX5

- **Setup:** Configured-state run at AX5. Use a vocabulary with long words (for example, "uncomfortable", "breakfast", "wheelchair") and a message of at least eight words.
- **Steps:**
  1. Inspect every cell on two vocabulary pages for truncated ("...") or clipped text.
  2. Build the eight-word message and inspect the message bar.
  3. Check whether the message bar wraps, scrolls, or shrinks text to show the full message, and whether that behavior is documented.
- **Expected result:** No word in a cell is truncated or clipped. The message bar shows the full message by wrapping or by scrolling with a visible indication that more text exists.
- **Pass criterion:** At AX5, no cell label is truncated or clipped, and the full message in the message bar can be read through wrapping or documented scrolling.
- **Fail criterion:** Any cell label is truncated or clipped, or any part of the message cannot be read in the message bar.
- **Evidence to record:** Screenshots of each page and the message bar at AX5, with truncations circled.
- **Maps to:** WCAG 2.2 1.4.4 Resize Text (Level AA); WCAG 2.2 1.4.10 Reflow (Level AA); WCAG 2.2 1.4.12 Text Spacing (Level AA).

### DT-03 Layout stays usable at the largest sizes

- **Setup:** Configured-state run at AX5, in both portrait and landscape.
- **Steps:**
  1. Inspect the communication screen for overlapping text or controls.
  2. Confirm the speak, delete, clear, and home controls are still visible and reachable.
  3. Open two sheets or menus and confirm their controls, including close or cancel, are visible.
  4. Rotate the device and repeat.
- **Expected result:** No text or controls overlap, and no control is pushed off screen or hidden. If content must scroll, scrolling is possible and obvious.
- **Pass criterion:** At AX5, in both orientations, no controls overlap and every control is visible or reachable by scrolling.
- **Fail criterion:** Any controls overlap, or any control is pushed off screen with no way to reach it.
- **Evidence to record:** Screenshots in both orientations.
- **Maps to:** WCAG 2.2 1.4.10 Reflow (Level AA); WCAG 2.2 1.3.4 Orientation (Level AA); WCAG 2.2 2.4.11 Focus Not Obscured (Minimum) (Level AA).

### DT-04 The app's own text size control does not conflict with Dynamic Type

- **Setup:** Configured-state run. The app has its own text or label size setting. If not, record Not Applicable.
- **Steps:**
  1. Set the app's text size to its largest and Dynamic Type to default. Capture a screenshot.
  2. Set Dynamic Type to AX5 with the app's text size at its largest. Capture a screenshot.
  3. Set the app's text size to its smallest and Dynamic Type to AX5. Capture a screenshot.
  4. Read the app's documentation on how the two settings combine.
- **Expected result:** The combination is predictable and documented (for example, the app setting is relative to Dynamic Type, or the app setting overrides it for cells only). No combination produces unreadable or clipped text.
- **Pass criterion:** The interaction between the two settings is documented and observed to match the documentation, and no tested combination produces clipped or overlapping text.
- **Fail criterion:** The interaction is undocumented or does not match the documentation, or any tested combination produces clipped or overlapping text.
- **Evidence to record:** Three screenshots; quote or screenshot of documentation.
- **Maps to:** WCAG 2.2 1.4.4 Resize Text (Level AA); Revised Section 508 503.2 User Preferences.

### DT-05 Settings and caregiver screens also scale

- **Setup:** Configured-state run at AX5. Unlock any supervisor or edit mode.
- **Steps:**
  1. Open the app's settings, the vocabulary editor, and any caregiver or supervisor screens.
  2. Inspect text size, truncation, and overlap.
- **Expected result:** Settings, editor, and caregiver screens scale with Dynamic Type and remain readable and usable.
- **Pass criterion:** All tested settings, editor, and caregiver screens scale at AX5 with no truncation that hides meaning and no overlapping controls.
- **Fail criterion:** Any tested screen ignores Dynamic Type, or truncation or overlap hides meaning or controls.
- **Evidence to record:** Screenshots of each screen at AX5.
- **Maps to:** WCAG 2.2 1.4.4 Resize Text (Level AA); WCAG 2.2 1.4.10 Reflow (Level AA).

## 4.6 Reduce Motion (RM)

### Why reduced motion matters for AAC users

Some AAC users have vestibular disorders, seizure disorders, sensory processing differences, or visual processing differences, including cortical visual impairment. Sliding pages, bouncing cells, and animated symbols can cause dizziness, distraction, or distress, and can make it harder to find the next word. The platform Reduce Motion setting tells apps to remove or soften motion.

### Reduce Motion user needs covered

- AAC users with vestibular disorders or motion sensitivity.
- AAC users with cortical visual impairment or attention differences for whom motion is distracting.
- AAC users with photosensitive conditions.

### RM-01 Page transitions and cell animations crossfade or stop

- **Setup:** Configured-state run. Record a page change and a cell selection with Reduce Motion off, then turn Reduce Motion on.
- **Steps:**
  1. With Reduce Motion on, change pages three times, open and close a folder, and select three cells.
  2. Compare the recordings with Reduce Motion off and on.
- **Expected result:** With Reduce Motion on, sliding, zooming, and bouncing are replaced by a crossfade or an instant change. Cell selection feedback uses a color or border change rather than scaling or bouncing.
- **Pass criterion:** With Reduce Motion on, no page transition or cell selection uses sliding, zooming, or bouncing motion.
- **Fail criterion:** Any page transition or cell selection still slides, zooms, or bounces with Reduce Motion on.
- **Evidence to record:** Screen recordings with Reduce Motion off and on.
- **Maps to:** WCAG 2.2 2.3.3 Animation from Interactions (Level AAA); Revised Section 508 503.2 User Preferences; Apple HIG Accessibility (Reduce Motion).

### RM-02 Symbols do not autoplay animation

- **Setup:** Configured-state run with Reduce Motion on. Include any animated symbols, animated mascots, or video cells the app offers.
- **Steps:**
  1. Open pages with animated content and observe for 10 seconds.
  2. Turn Reduce Motion off and repeat, for comparison.
  3. Check whether animated content can be paused or turned off in the app.
- **Expected result:** With Reduce Motion on, animated symbols show a still image. Any animation that plays for more than 5 seconds can be paused, stopped, or hidden regardless of Reduce Motion.
- **Pass criterion:** With Reduce Motion on, no symbol or decorative element animates automatically, and any animation longer than 5 seconds can be paused or turned off in the app.
- **Fail criterion:** Any symbol or decorative element animates automatically with Reduce Motion on, or an animation longer than 5 seconds cannot be paused or turned off.
- **Evidence to record:** Screen recordings with Reduce Motion on and off.
- **Maps to:** WCAG 2.2 2.2.2 Pause, Stop, Hide (Level A); WCAG 2.2 2.3.1 Three Flashes or Below Threshold (Level A).

### RM-03 No parallax, and the app's own animation setting is honored

- **Setup:** Configured-state run with Reduce Motion on. Note whether the app has its own animation setting.
- **Steps:**
  1. Tilt and move the device while viewing the communication and home screens, and watch for parallax or motion-driven effects.
  2. If the app has its own animation setting, turn it off with Reduce Motion off, and confirm animations stop.
  3. Turn the app's animation setting on with Reduce Motion on, and record which setting wins and whether that is documented.
- **Expected result:** No parallax or device-motion effects appear with Reduce Motion on. The app's own animation setting, if present, works, and its relationship with Reduce Motion is documented. Platform Reduce Motion is never overridden to add motion without the user's explicit choice.
- **Pass criterion:** No parallax or motion-driven effects appear with Reduce Motion on, and any app animation setting works as documented.
- **Fail criterion:** Parallax or motion-driven effects appear with Reduce Motion on, or the app's animation setting does not work or is undocumented.
- **Evidence to record:** Screen recording (or a second camera) while tilting; screenshots of settings.
- **Maps to:** WCAG 2.2 2.3.3 Animation from Interactions (Level AAA); WCAG 2.2 2.5.4 Motion Actuation (Level A).

## 4.7 High contrast and color independence (HC)

### Why contrast and color independence matter for AAC users

Many AAC systems color-code cells by part of speech or category. Color coding helps many users, but it fails users who are color blind, who have low vision, or who use Smart Invert or dark mode, if color is the only cue. Low-contrast labels, borders, and highlights make cells hard to find. Contrast is measured on real screenshots from the device, not on design files, because the rendered result is what the user sees.

### Contrast user needs covered

- AAC users and partners with low vision.
- AAC users and partners with color vision deficiencies.
- Users of Increase Contrast, Smart Invert, and dark mode.
- Users with cortical visual impairment who rely on high-contrast presentation.

### HC-01 Text contrast meets 4.5:1, or 3:1 for large text

- **Setup:** Configured-state run in light mode, then dark mode. Capture full-screen screenshots of the communication screen with every cell background color in use, plus the message bar and toolbar.
- **Steps:**
  1. For each distinct text and background color pair, sample the colors from the screenshot with a contrast tool.
  2. Record the contrast ratio.
  3. Classify text as large (at least 18 point regular or 14 point bold) or normal.
- **Expected result:** Normal text has at least 4.5:1 contrast with its background; large text has at least 3:1.
- **Pass criterion:** Every tested text and background pair meets 4.5:1 for normal text or 3:1 for large text, in both light and dark mode.
- **Fail criterion:** Any tested text and background pair falls below the required ratio in either mode.
- **Evidence to record:** Screenshots; a table of color pairs with measured ratios; tool name.
- **Maps to:** WCAG 2.2 1.4.3 Contrast (Minimum) (Level AA); Apple HIG Accessibility (color and contrast).

### HC-02 Cell borders, scan highlight, and focus ring meet 3:1

- **Setup:** Configured-state run in light and dark mode. Capture screenshots with a selected cell, the scan highlight (if the app scans), and VoiceOver focus visible.
- **Steps:**
  1. Measure the contrast of cell borders against the background (where borders are needed to identify a cell).
  2. Measure the scan highlight and selection indicator against adjacent colors.
  3. Measure icons that convey meaning without text (for example, a speak icon) against their background.
- **Expected result:** Each graphical element needed to identify or operate a control has at least 3:1 contrast against adjacent colors.
- **Pass criterion:** Every tested border, highlight, selection indicator, and meaningful icon has at least 3:1 contrast against adjacent colors in both modes.
- **Fail criterion:** Any tested element needed to identify or operate a control falls below 3:1 in either mode.
- **Evidence to record:** Screenshots with measured ratios.
- **Maps to:** WCAG 2.2 1.4.11 Non-text Contrast (Level AA); WCAG 2.2 2.4.7 Focus Visible (Level AA).

### HC-03 The Increase Contrast setting is honored

- **Setup:** Configured-state run. Capture screenshots with Increase Contrast off, then on.
- **Steps:**
  1. Compare cell borders, text, toolbar icons, and the message bar between the two screenshots.
  2. Measure the contrast of the lowest-contrast text pair from HC-01 with Increase Contrast on.
- **Expected result:** With Increase Contrast on, the app increases contrast of text, borders, or separators, or the app's default contrast already meets at least 7:1 for text. System controls used by the app show their higher-contrast appearance.
- **Pass criterion:** With Increase Contrast on, the app shows a visible increase in contrast, or all text already meets 7:1.
- **Fail criterion:** The app looks identical with Increase Contrast on and off, and some text is below 7:1.
- **Evidence to record:** Paired screenshots; measured ratios.
- **Maps to:** WCAG 2.2 1.4.6 Contrast (Enhanced) (Level AAA); Revised Section 508 503.2 User Preferences; Apple HIG Accessibility (Increase Contrast).

### HC-04 Color is never the only cue

- **Setup:** Configured-state run. Convert screenshots to grayscale (with an image editor, or by turning on the platform's grayscale color filter and capturing screenshots).
- **Steps:**
  1. In grayscale, identify which cell is selected.
  2. In grayscale, identify the current scan position.
  3. In grayscale, identify the category or part of speech of five cells, if the app color-codes cells.
  4. Identify any error or warning states in grayscale.
- **Expected result:** Selected state, scan position, and error states are shown with a non-color cue (border thickness, shape, icon, text, or pattern) in addition to color.
- **Pass criterion:** Selected state, scan position, and error states can each be identified in grayscale.
- **Fail criterion:** Any of selected state, scan position, or error state can be identified only by color.
- **Evidence to record:** Color and grayscale screenshots side by side.
- **Maps to:** WCAG 2.2 1.4.1 Use of Color (Level A); Revised Section 508 302.3 Without Perception of Color.

### HC-05 Smart Invert and dark mode keep symbols and text readable

- **Setup:** Configured-state run. Capture screenshots in light mode, dark mode, and with Smart Invert on.
- **Steps:**
  1. With Smart Invert on, inspect symbol images and photographs in cells: are they shown in their original colors or inverted?
  2. In dark mode and Smart Invert, inspect text for readability and measure contrast.
  3. Inspect the message bar and any symbols shown in it.
- **Expected result:** Symbol images and photographs are not inverted (they keep original colors), while text and backgrounds adapt and remain readable.
- **Pass criterion:** With Smart Invert on and in dark mode, symbol images keep their original colors and all tested text meets the HC-01 ratios.
- **Fail criterion:** Symbol images or photographs are inverted into negative colors, or text becomes unreadable or falls below HC-01 ratios.
- **Evidence to record:** Screenshots in all three modes.
- **Maps to:** WCAG 2.2 1.4.3 Contrast (Minimum) (Level AA); WCAG 2.2 1.1.1 Non-text Content (Level A); Apple HIG Accessibility (Smart Invert).

### HC-06 Symbol background color coding has a secondary cue

- **Setup:** Configured-state run with the app's color coding scheme turned on (for example, by part of speech). If the app has no color coding, record Not Applicable.
- **Steps:**
  1. Review the app's documentation for its color coding scheme.
  2. Check whether each coded category has a secondary cue (border style, icon, position in the grid, or a label) or whether the scheme is presented as a supplement to the word.
  3. Check whether the color scheme can be changed or turned off.
- **Expected result:** Color coding is never the only way to know a cell's category where that category matters to operation, and the user or caregiver can change or turn off the scheme.
- **Pass criterion:** Each color-coded category has a secondary non-color cue or is not needed to operate the app, and the color scheme can be changed or turned off.
- **Fail criterion:** A category needed to operate the app is shown only by color, or the color scheme cannot be changed or turned off.
- **Evidence to record:** Screenshots; documentation of the scheme.
- **Maps to:** WCAG 2.2 1.4.1 Use of Color (Level A); WCAG 2.2 1.3.3 Sensory Characteristics (Level A).

## 4.8 Emergency and safety vocabulary (EM)

### Why emergency vocabulary matters for AAC users

A person who uses AAC must be able to say "help", "stop", "pain", "I'm sick", or "I can't breathe" at any time, from any screen, with the access method they use, even when the app is locked down for a classroom or the network is down. No other app category carries this responsibility. These tests are written so that a failure is almost always rated Critical.

When testing emergency phrases with a participant, explain first that it is a test, avoid public settings where the phrases could cause alarm, and never ask a participant to repeat distressing content.

### Emergency vocabulary user needs covered

- Every AAC user, under every access method.
- Users in supervised settings (school, hospital, residential care) where the app may be locked down.
- Communication partners who must understand an urgent message immediately.

### EM-01 Emergency vocabulary exists and is reachable in two actions from any screen

- **Setup:** Configured-state run with default vocabulary. Identify the emergency, help, pain, or stop vocabulary set the app provides.
- **Steps:**
  1. From the home screen, count the number of selections needed to speak "help" (or the app's equivalent).
  2. Navigate three levels deep into folders, then count selections needed to speak "help".
  3. Open a sheet or menu, then count selections needed to speak "help".
  4. Repeat for "stop" and "pain" (or equivalents).
- **Expected result:** A help, stop, pain, or emergency vocabulary set exists, and from any screen the user can speak an emergency phrase in at most two actions (for example, one action to open the emergency set and one to speak the phrase, or one action on an always-visible emergency button).
- **Pass criterion:** Emergency vocabulary exists, and from every tested screen an emergency phrase can be spoken in at most two actions.
- **Fail criterion:** No emergency vocabulary exists by default, or from any tested screen more than two actions are needed to speak an emergency phrase.
- **Evidence to record:** Screen recording with audio from each starting screen; written action counts.
- **Maps to:** WCAG 2.2 3.2.6 Consistent Help (Level A); WCAG 2.2 2.4.1 Bypass Blocks (Level A).

### EM-02 Emergency vocabulary is reachable with VoiceOver

- **Setup:** Configured-state run with VoiceOver on.
- **Steps:**
  1. From the home screen and from three levels deep, find and speak an emergency phrase using only VoiceOver gestures.
  2. Count the number of swipes or gestures needed.
  3. Check whether the emergency area is reachable through a heading, the rotor, or a consistent position (for example, the first or last element).
- **Expected result:** The emergency area is quickly findable with VoiceOver from every screen, through a consistent position, heading, or rotor option, and the phrase can be spoken.
- **Pass criterion:** From every tested screen, an emergency phrase can be found and spoken using only VoiceOver, through a consistent position, heading, or rotor option.
- **Fail criterion:** From any tested screen, the emergency phrase cannot be reached with VoiceOver, or can only be found by swiping through the whole grid.
- **Evidence to record:** Screen recording with audio; gesture counts.
- **Maps to:** WCAG 2.2 2.4.1 Bypass Blocks (Level A); WCAG 2.2 3.2.6 Consistent Help (Level A); WCAG 2.2 4.1.2 Name, Role, Value (Level A).

### EM-03 Emergency vocabulary is reachable with switch scanning and with gaze

- **Setup:** Configured-state run. Test with the app's own scanner, with iPadOS Switch Control, and with gaze and dwell, as each is available.
- **Steps:**
  1. With each access method, from the home screen and from three levels deep, reach and speak an emergency phrase.
  2. Time how long it takes at a typical scan rate (for example, 1.5 seconds per item) or dwell setting (for example, 1 second).
  3. Check whether the scanner offers a fast path to the emergency area (for example, it is scanned first, or a dedicated switch goes to it).
- **Expected result:** Under each access method, the emergency phrase can be reached and spoken from every screen, within one scan cycle or a few gaze selections.
- **Pass criterion:** Under every tested access method, an emergency phrase can be spoken from every tested screen without touch, within one full scan cycle or three gaze selections.
- **Fail criterion:** Under any tested access method, an emergency phrase cannot be reached without touch, or takes longer than one full scan cycle or three gaze selections.
- **Evidence to record:** Screen recordings with audio for each access method; measured times.
- **Maps to:** WCAG 2.2 2.1.1 Keyboard (Level A); WCAG 2.2 3.2.6 Consistent Help (Level A); Revised Section 508 302.7 With Limited Manipulation.

### EM-04 Emergency vocabulary works in Guided Access and in student or kiosk modes

- **Setup:** Configured-state run. Start a Guided Access session with the communication screen. If the app has a student, kiosk, or restricted mode, test that separately with its most restrictive settings.
- **Steps:**
  1. In Guided Access, speak an emergency phrase.
  2. In the app's student or kiosk mode, speak an emergency phrase.
  3. Check whether any setting in these modes hides or disables the emergency area.
- **Expected result:** Emergency vocabulary is available and speaks in Guided Access and in every app restricted mode. If a mode can hide the emergency area, the app warns the supervisor before allowing it.
- **Pass criterion:** An emergency phrase can be spoken in Guided Access and in every app restricted mode at its most restrictive setting.
- **Fail criterion:** An emergency phrase cannot be spoken in Guided Access or in any app restricted mode.
- **Evidence to record:** Screen recordings with audio; screenshots of restricted mode settings.
- **Maps to:** WCAG 2.2 3.2.6 Consistent Help (Level A); Apple accessibility documentation (Guided Access).

### EM-05 Emergency speech plays at a usable volume

- **Setup:** Configured-state run. Set the app's own speech volume to its lowest non-muted level (if the app has a volume control) and the device volume to a low level.
- **Steps:**
  1. Speak an emergency phrase and measure loudness with a sound level meter app on a second device at 1 meter, or record a subjective rating.
  2. Speak a non-emergency phrase at the same settings, for comparison.
  3. Read the app's documentation on emergency phrase volume.
- **Expected result:** Emergency phrases play at full volume regardless of the app's current volume setting, or the app clearly documents its emergency volume behavior and offers a setting to raise emergency volume.
- **Pass criterion:** Emergency phrases play louder than, or at the same level as, the app's maximum normal speech volume, or the app documents its emergency volume behavior and provides a setting to raise it.
- **Fail criterion:** Emergency phrases play at the same low volume as other speech with no documented behavior or setting, or are silent.
- **Evidence to record:** Screen recording with audio; sound level measurements if taken; documentation.
- **Maps to:** WCAG 2.2 1.4.2 Audio Control (Level A); Revised Section 508 302.5 With Limited Hearing.

### EM-06 Emergency vocabulary cannot be hidden or deleted by a non-supervisor

- **Setup:** Configured-state run with the supervisor or edit lock turned on (see CC-01).
- **Steps:**
  1. As a user without the supervisor passcode, attempt to hide, move, or delete the emergency cells or set by every path available (long press, edit mode, settings, drag).
  2. With the supervisor passcode, attempt to hide or delete the emergency set and note any warning shown.
- **Expected result:** Without supervisor access, emergency vocabulary cannot be hidden, moved, or deleted. A supervisor who tries to remove it sees a warning about the safety impact.
- **Pass criterion:** Emergency vocabulary cannot be hidden, moved, or deleted without supervisor access.
- **Fail criterion:** Any path allows a non-supervisor to hide, move, or delete emergency vocabulary.
- **Evidence to record:** Screen recording of each attempt; screenshot of any supervisor warning.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA).

### EM-07 Emergency vocabulary works offline

- **Setup:** Configured-state run. Turn on Airplane Mode and turn off Wi-Fi.
- **Steps:**
  1. Force quit and relaunch the app.
  2. Speak each emergency phrase in the default emergency set.
- **Expected result:** Every emergency phrase speaks offline with the selected voice, or with a clearly documented offline fallback voice.
- **Pass criterion:** Every emergency phrase speaks offline after relaunch.
- **Fail criterion:** Any emergency phrase fails to speak, or speaks only after a delay of more than 2 seconds, offline.
- **Evidence to record:** Screen recording with audio showing Airplane Mode in the status bar or Control Center.
- **Maps to:** Revised Section 508 302.6 Without Speech; WCAG 2.2 3.2.6 Consistent Help (Level A).

## 4.9 Speech output (SP)

### Why speech output matters for AAC users

Speech output is how the AAC user is heard. The wrong language, a voice that changes without warning, a message that cannot be stopped, or speech that goes silent because the device is on Silent all change or block what the person says. Speech must be predictable, controllable, and audible in the places the person lives, learns, and works.

### Speech output user needs covered

- Every AAC user who relies on speech output to be heard.
- Multilingual AAC users and families.
- Users in noisy environments or who use external speakers.
- Communication partners who are hard of hearing.

### SP-01 The speaking language matches the vocabulary language

- **Setup:** Configured-state run. Configure one vocabulary set in a language other than the device language, if supported, and a multilingual board if the app supports one.
- **Steps:**
  1. Speak ten words from the vocabulary set and note the language and accent of the speech.
  2. On a multilingual board, speak words from each language and note whether each is spoken in its own language.
  3. Change the device language and repeat step 1.
- **Expected result:** Words are spoken in the language of the vocabulary, not the device language. On a multilingual board, each word is spoken in its own language's voice.
- **Pass criterion:** Every tested word is spoken in the language of its vocabulary, regardless of device language.
- **Fail criterion:** Any tested word is spoken in the wrong language or with another language's pronunciation rules.
- **Evidence to record:** Screen recording with audio; list of words and the language heard.
- **Maps to:** WCAG 2.2 3.1.1 Language of Page (Level A); WCAG 2.2 3.1.2 Language of Parts (Level AA).

### SP-02 The selected voice is used consistently and can be chosen

- **Setup:** Configured-state run.
- **Steps:**
  1. Open voice settings and confirm the user or caregiver can choose among available voices.
  2. Select a voice. Speak single words, a full message, an emergency phrase, and a phrase from a quick phrases area (if present).
  3. Force quit and relaunch, then repeat step 2.
  4. Note whether any speech uses a different voice.
- **Expected result:** The user or caregiver can choose the voice, and every kind of speech in the app uses the chosen voice, before and after relaunch.
- **Pass criterion:** A voice can be chosen, and every tested kind of speech uses the chosen voice before and after relaunch.
- **Fail criterion:** No voice choice is offered, or any tested speech uses a different voice than the one chosen.
- **Evidence to record:** Screen recording with audio; screenshot of voice settings.
- **Maps to:** Revised Section 508 503.2 User Preferences; Revised Section 508 302.6 Without Speech.

### SP-03 Speech can be interrupted

- **Setup:** Configured-state run. Build a message of at least 15 words.
- **Steps:**
  1. Speak the message. After about one second, select a new word.
  2. Speak the message again. After about one second, activate a stop or clear control, if present.
  3. Repeat both steps with VoiceOver on and with a switch scanner.
  4. Read the documentation on interruption behavior.
- **Expected result:** A new selection or a stop control interrupts speech promptly (within about half a second), and the behavior is documented. The user is never forced to wait for a long message to finish before saying something new.
- **Pass criterion:** Speech stops within 0.5 seconds of a stop control or new selection, under touch and under each tested access method.
- **Fail criterion:** Speech cannot be interrupted, or continues for more than 0.5 seconds after a stop control or new selection.
- **Evidence to record:** Screen recording with audio; measured stop times from the recording.
- **Maps to:** WCAG 2.2 1.4.2 Audio Control (Level A); WCAG 2.2 2.2.2 Pause, Stop, Hide (Level A).

### SP-04 The message can be replayed

- **Setup:** Configured-state run. Build and speak a message.
- **Steps:**
  1. After the message has been spoken, activate the speak control again without changing the message.
  2. Clear the message, then check for a way to replay the last spoken message (for example, a history or repeat control).
- **Expected result:** The current message can be spoken again on demand. A recently spoken message can be recovered or replayed after clearing, through a history or repeat feature, or the absence is documented.
- **Pass criterion:** The current message can be replayed on demand, and the last spoken message can be replayed after clearing or the absence of this feature is documented.
- **Fail criterion:** The current message cannot be replayed, or the last message is lost on clearing with no replay feature and no documentation.
- **Evidence to record:** Screen recording with audio.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA); Revised Section 508 302.6 Without Speech.

### SP-05 Speak-on-tap and speak-on-message modes are predictable

- **Setup:** Configured-state run. Identify the app's speech modes (for example, speak each word on selection, speak only when the message is spoken, or both).
- **Steps:**
  1. In each mode, select three words and speak the message, noting exactly when speech occurs.
  2. Switch modes and confirm the change takes effect immediately and persists after relaunch.
  3. Confirm the current mode is shown or can be found in settings.
- **Expected result:** Each mode behaves exactly as described in settings or documentation, every time. The current mode can be identified.
- **Pass criterion:** Each speech mode behaves as documented in every repetition, and the current mode can be identified in the app.
- **Fail criterion:** Any mode speaks when its description says it should not, or stays silent when it should speak, or the current mode cannot be identified.
- **Evidence to record:** Screen recording with audio of each mode; screenshots of settings.
- **Maps to:** WCAG 2.2 3.2.2 On Input (Level A); WCAG 2.2 3.2.1 On Focus (Level A).

### SP-06 Speech rate and pitch are adjustable

- **Setup:** Configured-state run.
- **Steps:**
  1. Open speech settings and record the available rate and pitch controls and their ranges.
  2. Set rate to minimum and maximum and speak a ten-word message each time.
  3. Set pitch to minimum and maximum (if available) and speak again.
  4. Confirm settings persist after relaunch.
- **Expected result:** Rate is adjustable across a noticeable range, pitch is adjustable if the voice supports it, both changes are audible, and they persist.
- **Pass criterion:** Speech rate can be adjusted with an audible change between minimum and maximum, and the setting persists after relaunch.
- **Fail criterion:** Rate cannot be adjusted, the change is not audible, or the setting does not persist.
- **Evidence to record:** Screen recording with audio at each setting; screenshots of settings.
- **Maps to:** Revised Section 508 503.2 User Preferences; WCAG 2.2 1.4.2 Audio Control (Level A).

### SP-07 Audio routes to headphones and Bluetooth speakers

- **Setup:** Configured-state run. Have wired headphones (or an adapter), Bluetooth headphones, and a Bluetooth speaker available, as possible.
- **Steps:**
  1. Connect each output device in turn and speak a message.
  2. Disconnect the device mid-message and note what happens.
  3. Speak a message after disconnecting and confirm audio returns to the built-in speaker.
- **Expected result:** Speech plays through the connected output device. On disconnect, speech continues or resumes through the built-in speaker without the user needing to restart the app.
- **Pass criterion:** Speech plays through each connected output device, and after disconnecting, the next message plays through the built-in speaker without restarting the app.
- **Fail criterion:** Speech does not play through a connected device, or after disconnecting, speech is silent until the app is restarted.
- **Evidence to record:** Written observations with device classes tested (wired, Bluetooth headphones, Bluetooth speaker); video from a second camera if helpful.
- **Maps to:** Revised Section 508 302.5 With Limited Hearing; Revised Section 508 502.2.2 No Disruption of Accessibility Features.

### SP-08 Speech is audible with the Silent switch or Focus mode on, or the behavior is documented

- **Setup:** Configured-state run. On devices with a Silent switch or Ring and Silent control, set it to Silent. Separately, turn on a Focus mode (for example, Do Not Disturb).
- **Steps:**
  1. With Silent on, speak a message and an emergency phrase.
  2. With Focus on, speak a message and an emergency phrase.
  3. Read the app's documentation on Silent and Focus behavior.
- **Expected result:** Speech output is audible with Silent or Focus on, because the user's voice is not a notification sound. If the app chooses to follow Silent, it clearly documents this and warns the user.
- **Pass criterion:** Messages and emergency phrases are audible with Silent on and with Focus on, or the app clearly documents and visibly indicates that speech is silenced.
- **Fail criterion:** Speech is silent with Silent or Focus on, and the app gives no documentation or visible indication.
- **Evidence to record:** Screen recording with audio, or second-camera video showing the Silent setting.
- **Maps to:** Revised Section 508 302.6 Without Speech; WCAG 2.2 1.4.2 Audio Control (Level A).

### SP-09 Speech works after the app is backgrounded and returned

- **Setup:** Configured-state run. Build a message.
- **Steps:**
  1. Switch to another app for 30 seconds, then return. Speak the message.
  2. Lock the device for 5 minutes, unlock, and return to the app. Speak the message.
  3. Play audio in another app (for example, music), return, and speak the message.
- **Expected result:** The message is preserved and speaks normally after each interruption. Audio from other apps is paused or ducked so the message is heard.
- **Pass criterion:** After each interruption, the message is intact and speaks within 1 second of activation.
- **Fail criterion:** After any interruption, the message is lost, speech is silent, or speech is delayed more than 1 second.
- **Evidence to record:** Screen recording with audio.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA); Revised Section 508 302.6 Without Speech.

## 4.10 Offline operation (OF)

### Why offline operation matters for AAC users

AAC users need to communicate on the school bus, in hospitals, in rural areas, on planes, during outages, and in places where Wi-Fi is blocked. An app that needs a network connection to speak takes away the user's voice whenever the network goes away. Offline operation is a core reliability requirement, not a convenience.

### Offline user needs covered

- Every AAC user who travels or lives in an area with unreliable connectivity.
- Students in schools with restricted or filtered networks.
- Users in hospitals and care settings where devices may be kept offline.

### OF-01 Full vocabulary and speech work in Airplane Mode

- **Setup:** Configured-state run after initial setup is complete and voices are downloaded. Turn on Airplane Mode and confirm Wi-Fi and Bluetooth are off.
- **Steps:**
  1. Force quit and relaunch the app.
  2. Navigate to at least five different vocabulary pages, including folders at least two levels deep.
  3. Build and speak a message on each page.
  4. Use word prediction, keyboard, and any quick phrases, if present.
- **Expected result:** Every vocabulary page, symbol, and speech function used during communication works offline.
- **Pass criterion:** All tested pages display their symbols, and all tested messages speak, in Airplane Mode after relaunch.
- **Fail criterion:** Any page fails to load, any symbol is missing, or any message fails to speak in Airplane Mode.
- **Evidence to record:** Screen recording with audio showing Airplane Mode active.
- **Maps to:** Revised Section 508 302.6 Without Speech; EN 301 549 clause 4 functional performance statements.

### OF-02 Downloaded voices are available offline

- **Setup:** Configured-state run. Download at least one high-quality voice offered by the app or the platform, and select it. Turn on Airplane Mode.
- **Steps:**
  1. Relaunch the app and speak a message.
  2. Confirm the selected voice is used, not a fallback voice.
  3. Open voice settings and check how online-only voices are marked.
- **Expected result:** Downloaded voices work offline. Voices that need a connection are clearly marked as online-only in voice settings.
- **Pass criterion:** The downloaded voice speaks offline, and any online-only voice is clearly marked as such.
- **Fail criterion:** A downloaded voice does not work offline, the app silently switches to another voice, or online-only voices are not marked.
- **Evidence to record:** Screen recording with audio; screenshot of voice settings.
- **Maps to:** Revised Section 508 503.2 User Preferences; Revised Section 508 302.6 Without Speech.

### OF-03 No login wall appears offline after initial setup

- **Setup:** Configured-state run with an account signed in, if the app uses accounts. Turn on Airplane Mode.
- **Steps:**
  1. Force quit and relaunch the app.
  2. Leave the device offline for at least 24 hours if practical (or change nothing and relaunch several times), then relaunch.
  3. Check whether the app asks for a login, subscription check, or license check before allowing communication.
- **Expected result:** The app opens straight to communication offline. Account, subscription, or license checks never block core communication offline.
- **Pass criterion:** The app opens to the communication screen offline without any login, subscription, or license prompt that blocks communication.
- **Fail criterion:** Any login, subscription, or license prompt blocks communication while offline.
- **Evidence to record:** Screen recording of each relaunch; note of how long the device was offline.
- **Maps to:** WCAG 2.2 3.3.8 Accessible Authentication (Minimum) (Level AA); Revised Section 508 302.6 Without Speech.

### OF-04 Offline edits persist and survive reconnection

- **Setup:** Configured-state run with cloud sync turned on, if the app offers it. Turn on Airplane Mode.
- **Steps:**
  1. Unlock edit mode and add a new word cell, rename an existing cell, and move a cell.
  2. Force quit and relaunch offline. Confirm the edits are present.
  3. Turn off Airplane Mode and wait for sync to complete (or 5 minutes).
  4. Confirm the edits are still present and nothing else changed. If a second synced device is available, confirm the edits arrive there without duplicates.
- **Expected result:** Offline edits are saved immediately, survive relaunch, and are not lost, duplicated, or corrupted when connectivity returns.
- **Pass criterion:** All three edits persist after offline relaunch and after reconnection, with no lost, duplicated, or altered cells.
- **Fail criterion:** Any edit is lost, duplicated, or altered, or any other vocabulary is changed, after relaunch or reconnection.
- **Evidence to record:** Screenshots before and after each step; screen recording of reconnection.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA).

### OF-05 The app launches offline after a device restart

- **Setup:** Configured-state run. Turn on Airplane Mode.
- **Steps:**
  1. Restart the device fully (power off and on).
  2. Unlock the device, keep Airplane Mode on, and launch the app.
  3. Build and speak a message.
- **Expected result:** The app launches and communicates normally offline after a cold restart.
- **Pass criterion:** After a device restart in Airplane Mode, the app launches to the communication screen and speaks a message.
- **Fail criterion:** After a device restart in Airplane Mode, the app fails to launch, shows an error, or cannot speak.
- **Evidence to record:** Screen recording with audio from unlock through speech.
- **Maps to:** Revised Section 508 302.6 Without Speech.

## 4.11 Privacy (PR)

### Why privacy matters for AAC users

An AAC user's message history is a record of their speech: what they said, to whom, and when. Usage logs can reveal health conditions, emotions, relationships, and abuse disclosures. Many AAC users are children, and many have limited ability to understand or refuse data collection. Privacy failures in AAC are failures of the user's most personal data. These tests check what the app actually does on a real device and compare it with what the app says it does.

The privacy tests are observations, not legal opinions. Reviewers should consult their own counsel about legal obligations.

### Privacy user needs covered

- Every AAC user, and especially children and adults with guardians.
- Families who need to understand and control what is collected.
- School districts with obligations under student privacy laws.

### PR-01 No account is required for core communication

- **Setup:** Fresh install run.
- **Steps:**
  1. Launch the app and go through first-run setup, skipping or declining every account, sign-in, and email prompt.
  2. Attempt to build and speak a message.
  3. If an account is required, find the app's stated reason in its documentation or privacy policy.
- **Expected result:** Core communication (building and speaking messages with the included vocabulary) works without creating an account, or the app documents a specific reason why an account is required.
- **Pass criterion:** A message can be built and spoken without creating an account or signing in, or a specific documented reason for requiring an account is given.
- **Fail criterion:** An account is required for core communication and no specific reason is documented.
- **Evidence to record:** Screen recording of first-run setup; quote of any stated reason.
- **Maps to:** WCAG 2.2 3.3.8 Accessible Authentication (Minimum) (Level AA); App Store privacy labels.

### PR-02 Network traffic matches the privacy policy and privacy label

- **Setup:** Fresh install run and configured-state run. Configure a network proxy on the test device with its certificate trusted, or, if a proxy is not available, use the device's per-app cellular data usage view and record the limitation. Save a copy of the app's privacy policy and a screenshot of its App Store privacy label.
- **Steps:**
  1. Clear the proxy log. Launch the app and complete first-run setup.
  2. Use the app normally for 15 minutes: build and speak messages, navigate, open settings.
  3. Export the list of hosts the app contacted and the type of data sent (where visible).
  4. Classify each host: the app's own service, a platform service, a third-party analytics or advertising service, or unknown.
  5. Compare the list with the privacy policy and the privacy label.
- **Expected result:** Every host contacted is consistent with the privacy policy and privacy label. No message text, vocabulary selections, or usage logs are sent to any host not disclosed in the policy.
- **Pass criterion:** Every contacted host and every observed category of data sent is disclosed in the privacy policy and privacy label.
- **Fail criterion:** Any host or category of data is not disclosed, or message content is sent to a third party not named in the policy.
- **Evidence to record:** Proxy host list export; privacy policy copy with date; privacy label screenshot; comparison table.
- **Maps to:** App Store privacy labels; FERPA, COPPA, and GDPR transparency obligations as applicable (reviewer to determine).

### PR-03 Data at rest, backups, and message history are disclosed and controllable

- **Setup:** Configured-state run. Read the app's privacy policy and settings.
- **Steps:**
  1. Determine whether the app stores message history, and where (on device, in cloud, or both).
  2. Determine whether the app's data is protected by the device's data protection (for example, documented in the policy or security documentation).
  3. Determine whether the app's data is included in or excluded from device backups, and whether this is documented.
  4. Look for a setting that turns off message history storage, and test it: turn it off, speak three messages, and confirm they are not stored.
- **Expected result:** The app documents what it stores, where, and how it is protected, and whether it is included in backups. Message history storage can be turned off, and turning it off works.
- **Pass criterion:** Storage location, protection, and backup behavior are documented, and message history storage can be turned off and is observed not to store messages when off.
- **Fail criterion:** Storage location, protection, or backup behavior is undocumented, or message history cannot be turned off, or messages are stored when it is off.
- **Evidence to record:** Quotes from documentation; screenshots of settings; screen recording of the history test.
- **Maps to:** FERPA and state student privacy laws as applicable (reviewer to determine); EN 301 549 clause 12 documentation.

### PR-04 The user can delete history, data, and account, and retention is documented

- **Setup:** Configured-state run with message history, custom vocabulary, and an account (if used).
- **Steps:**
  1. Find and use the control to delete message history. Confirm it is gone.
  2. Find and use the control to delete user data (custom vocabulary and settings) after making a backup.
  3. If the app uses accounts, find the in-app account deletion path and confirm it can be started from inside the app.
  4. Read the privacy policy for retention periods for deleted data on servers and in server backups.
- **Expected result:** The user or caregiver can delete message history, user data, and the account from inside the app, and the policy states how long server copies are retained after deletion.
- **Pass criterion:** Message history, user data, and the account (if any) can each be deleted from inside the app, and server retention after deletion is documented.
- **Fail criterion:** Any of these cannot be deleted from inside the app, or retention after deletion is not documented.
- **Evidence to record:** Screen recordings of each deletion; quote of retention policy.
- **Maps to:** App Store account deletion requirement; GDPR right to erasure and COPPA deletion obligations as applicable (reviewer to determine).

### PR-05 Camera and microphone are requested only when needed, with plain consent

- **Setup:** Fresh install run.
- **Steps:**
  1. Go through first-run setup and normal communication. Note any camera, microphone, photo library, speech recognition, or location permission prompt and when it appears.
  2. Use a feature that needs the camera (for example, taking a photo for a cell) and note the prompt text.
  3. Deny the permission. Confirm the app still works for communication and explains how to enable the feature later.
  4. Read each permission purpose string for plain language.
- **Expected result:** No sensitive permission is requested at launch or during setup unless the feature is being used. Each prompt explains in plain language why the permission is needed. Denying the permission does not block communication.
- **Pass criterion:** Each sensitive permission is requested only when a feature that needs it is used, the prompt explains the purpose in plain language, and communication works after denial.
- **Fail criterion:** A sensitive permission is requested before the feature is used, the purpose is unclear, or denial blocks communication.
- **Evidence to record:** Screenshots of each prompt with its timing; screen recording after denial.
- **Maps to:** WCAG 2.2 3.3.2 Labels or Instructions (Level A); Apple HIG (requesting permission); COPPA as applicable (reviewer to determine).

### PR-06 No third-party analytics or ads in a student edition, or full disclosure

- **Setup:** Configured-state run of the edition marketed for students or schools. Use the PR-02 host list.
- **Steps:**
  1. Review the PR-02 host list for third-party analytics, advertising, attribution, or crash-reporting services.
  2. Use the app for 15 minutes and watch for any advertisement or promotional content.
  3. Compare findings with the privacy policy and any school data agreement.
- **Expected result:** A student edition shows no ads and sends no data to third-party analytics or advertising services, or any third-party service is fully disclosed with its purpose and the data it receives.
- **Pass criterion:** The student edition shows no ads and contacts no undisclosed third-party analytics or advertising service.
- **Fail criterion:** The student edition shows ads, or contacts a third-party analytics or advertising service that is not disclosed.
- **Evidence to record:** PR-02 host list with classifications; screenshots of any ads.
- **Maps to:** COPPA and state student privacy laws as applicable (reviewer to determine); App Store privacy labels.

### PR-07 Cloud sync is opt-in

- **Setup:** Fresh install run.
- **Steps:**
  1. Complete first-run setup with defaults, declining any optional prompts.
  2. Check settings to see whether cloud sync or cloud backup is on.
  3. Turn sync on and off and confirm the setting is respected (using the proxy host list if available).
- **Expected result:** Cloud sync and cloud backup are off until the user or caregiver turns them on, and turning them off stops uploads.
- **Pass criterion:** Cloud sync is off by default after setup with defaults, and turning it off stops sync traffic.
- **Fail criterion:** Cloud sync is on by default without an explicit choice, or turning it off does not stop sync traffic.
- **Evidence to record:** Screenshots of settings after setup; proxy observations if available.
- **Maps to:** GDPR data protection by default as applicable (reviewer to determine); App Store privacy labels.

### PR-08 Sharing or exporting a user's vocabulary needs an explicit action

- **Setup:** Configured-state run with custom vocabulary.
- **Steps:**
  1. Identify every way vocabulary, message history, or user data can leave the device (share sheet, export, sync to a clinician account, community sharing).
  2. For each, confirm it requires an explicit action and confirmation by the caregiver or user.
  3. Check whether any feature shares vocabulary publicly or to a community library by default.
- **Expected result:** Every way data leaves the device requires an explicit action. No vocabulary is shared publicly by default.
- **Pass criterion:** Every sharing or export path requires an explicit user or caregiver action, and nothing is shared publicly by default.
- **Fail criterion:** Any data leaves the device without an explicit action, or anything is shared publicly by default.
- **Evidence to record:** List of sharing paths; screenshots of confirmation prompts.
- **Maps to:** FERPA and GDPR as applicable (reviewer to determine); WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA).

### PR-09 Student privacy law checklist for the reviewer

- **Setup:** Desk review alongside the device findings from PR-01 to PR-08. This test produces a checklist record, not a legal conclusion.
- **Steps:**
  1. Record whether the vendor states its position on FERPA (United States, education records), including whether it acts as a "school official" under a district agreement.
  2. Record whether the vendor states its position on COPPA (United States, children under 13), including how parental or school consent is handled.
  3. Record whether the vendor addresses applicable state student privacy laws for the district's state.
  4. Record whether the vendor addresses GDPR or other regional laws if the app is used outside the United States.
  5. Note any gap between these statements and the device observations in PR-01 to PR-08.
- **Expected result:** The vendor provides written statements on each applicable framework, and those statements are consistent with observed behavior.
- **Pass criterion:** The vendor provides a written statement for each framework the reviewer identifies as applicable, and no statement contradicts the device observations.
- **Fail criterion:** The vendor provides no written statement for an applicable framework, or a statement contradicts the device observations.
- **Evidence to record:** Copies or links to vendor statements with dates; the reviewer's checklist. This is not legal advice.
- **Maps to:** FERPA; COPPA; state student privacy laws; GDPR (all as applicable, reviewer to determine).

### PR-10 A data processing or privacy agreement is available for districts

- **Setup:** Desk review. Contact the vendor's sales or privacy contact if needed.
- **Steps:**
  1. Ask for, or locate on the vendor's site, a data processing agreement, student data privacy agreement, or equivalent contract for schools.
  2. Record whether it covers data use limits, sub-processors, breach notification, data return and deletion at contract end, and security practices.
- **Expected result:** A written agreement is available for districts and covers the listed topics.
- **Pass criterion:** A written privacy or data processing agreement is available to districts and covers data use limits, sub-processors, breach notification, and data return and deletion at contract end.
- **Fail criterion:** No agreement is available, or it omits any of the listed topics.
- **Evidence to record:** Copy of the agreement or the vendor's written response, with date.
- **Maps to:** FERPA and state student privacy laws as applicable (reviewer to determine).

## 4.12 Clinician and caregiver controls (CC)

### Why caregiver controls matter for AAC users

AAC vocabularies are built over months or years. An accidental tap that deletes a folder, or a user exploring settings and changing the voice, can set communication back by weeks. At the same time, controls meant to protect the vocabulary must never block the user's voice, must never be bypassable by the very access method the user relies on, and must not turn into surveillance. Caregivers and clinicians also have their own access needs.

### Caregiver controls user needs covered

- AAC users who need their vocabulary protected from accidental changes.
- Caregivers, teachers, and clinicians who edit vocabulary, some with their own disabilities.
- Families moving between apps, schools, or clinicians who need their vocabulary to move with them.

### CC-01 An edit lock or supervisor mode protects vocabulary

- **Setup:** Configured-state run.
- **Steps:**
  1. Find the edit lock, supervisor mode, or passcode setting.
  2. Turn it on.
  3. Without unlocking, attempt to delete a cell, edit a cell, move a cell, change settings, and change the voice.
- **Expected result:** An edit lock exists, and when it is on, vocabulary and settings cannot be changed without unlocking.
- **Pass criterion:** An edit lock exists, and with it on, none of the tested changes can be made without unlocking.
- **Fail criterion:** No edit lock exists, or any tested change can be made with the lock on.
- **Evidence to record:** Screen recording of each attempt.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA).

### CC-02 The edit lock cannot be bypassed with touch or VoiceOver

- **Setup:** Configured-state run with the edit lock on.
- **Steps:**
  1. By touch, try long press, double tap, multi-finger gestures, and repeated tapping on the lock control and on cells.
  2. With VoiceOver, swipe through every element and try every custom action on cells and on the lock control.
  3. Check that VoiceOver does not reveal hidden edit controls or the passcode.
- **Expected result:** The lock cannot be bypassed by any touch gesture or any VoiceOver gesture or custom action.
- **Pass criterion:** No touch gesture, VoiceOver gesture, or VoiceOver custom action bypasses the edit lock or reveals the passcode.
- **Fail criterion:** Any touch gesture, VoiceOver gesture, or custom action bypasses the lock or reveals the passcode.
- **Evidence to record:** Screen recording with audio of each attempt.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA); WCAG 2.2 4.1.2 Name, Role, Value (Level A).

### CC-03 The edit lock cannot be bypassed with switch scanning or gaze

- **Setup:** Configured-state run with the edit lock on. Test with the app's scanner, with iPadOS Switch Control, and with gaze and dwell, as available.
- **Steps:**
  1. With each access method, scan or dwell over every element, including the lock control.
  2. Try sustained dwell, repeated switch presses, and the Switch Control menu actions (such as tap, hold, and gestures) on the lock control and cells.
- **Expected result:** No switch, Switch Control menu, or gaze action bypasses the lock. A lock that relies on a gesture (for example, a long hold) is not trivially triggered by a dwell or a Switch Control hold action.
- **Pass criterion:** No action available through the tested switch and gaze access methods bypasses the edit lock.
- **Fail criterion:** Any switch, Switch Control menu, or gaze action bypasses the edit lock.
- **Evidence to record:** Screen recordings for each access method.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA); Revised Section 508 502.2.2 No Disruption of Accessibility Features.

### CC-04 Supervisor mode never blocks emergency vocabulary

- **Setup:** Configured-state run with the edit lock on and every restriction the supervisor mode offers turned on.
- **Steps:**
  1. Speak an emergency phrase.
  2. Check whether any supervisor setting can hide or disable emergency vocabulary, and whether a warning appears.
- **Expected result:** Emergency vocabulary works with every supervisor restriction on. If a supervisor can hide it, the app warns before allowing it (see EM-06).
- **Pass criterion:** An emergency phrase can be spoken with every supervisor restriction on.
- **Fail criterion:** Any supervisor restriction prevents an emergency phrase from being spoken.
- **Evidence to record:** Screen recording with audio; screenshots of supervisor settings.
- **Maps to:** WCAG 2.2 3.2.6 Consistent Help (Level A).

### CC-05 Vocabulary backup and restore to a caregiver-controlled file

- **Setup:** Configured-state run with custom vocabulary (at least 10 custom cells, a custom folder, and a custom photo symbol). A second device or a fresh install is needed for restore.
- **Steps:**
  1. Create a backup to a file saved in a location the caregiver controls (for example, the Files app, a computer, or the caregiver's own cloud storage), not only the vendor's servers.
  2. Delete and reinstall the app (or use a second device).
  3. Restore from the backup file.
  4. Confirm every custom cell, folder, photo, and setting is restored.
- **Expected result:** The caregiver can create a backup file they control and restore from it fully.
- **Pass criterion:** A backup file can be saved to a caregiver-controlled location and a full restore from it brings back all tested custom content.
- **Fail criterion:** Backup is only possible to the vendor's servers, or a restore loses any tested custom content.
- **Evidence to record:** Screen recordings of backup and restore; before and after screenshots.
- **Maps to:** WCAG 2.2 3.3.4 Error Prevention (Legal, Financial, Data) (Level AA).

### CC-06 Vocabulary and data export in an open format

- **Setup:** Configured-state run with custom vocabulary.
- **Steps:**
  1. Find the export option for vocabulary and, if stored, usage data.
  2. Export and open the file on a computer.
  3. Determine whether the format is open and documented (for example, CSV, JSON, or a published open format for AAC boards) and whether it includes words, folder structure, and symbols or symbol references.
- **Expected result:** Vocabulary can be exported in an open, documented format that another app or a person could read, to support moving between apps.
- **Pass criterion:** Vocabulary can be exported in CSV, JSON, or another publicly documented open format, and the export includes words and folder structure.
- **Fail criterion:** No export exists, the only export is a proprietary undocumented format, or the export omits words or folder structure.
- **Evidence to record:** The exported file (with personal content removed); screenshots; link to format documentation.
- **Maps to:** Revised Section 508 602.3 Electronic Support Documentation; EN 301 549 clause 12 documentation.

### CC-07 Usage logging is disclosed, can be turned off, and is not presented as judgment

- **Setup:** Configured-state run. Identify any usage logging, data collection for progress reports, or language activity monitoring.
- **Steps:**
  1. Confirm logging is disclosed in the app (not only in the privacy policy) to the user and family.
  2. Turn logging off and confirm, by viewing reports or the PR-02 host list, that new usage is not logged.
  3. Check whether the user-facing communication screen shows any score, streak, rating, or judgment of the user's communication.
- **Expected result:** Logging is disclosed in the app, can be turned off, and stops when turned off. The user does not see scores or judgments about how they communicate on the communication screen.
- **Pass criterion:** Logging is disclosed in the app, stops when turned off, and no score or judgment of the user's communication appears on the communication screen.
- **Fail criterion:** Logging is undisclosed in the app, cannot be turned off, continues when off, or a score or judgment appears on the communication screen.
- **Evidence to record:** Screenshots of disclosure and settings; observations of logs after turning off.
- **Maps to:** FERPA and COPPA as applicable (reviewer to determine); App Store privacy labels.

### CC-08 Caregiver settings are usable with the caregiver's own access needs

- **Setup:** Configured-state run with the edit lock unlocked. Turn on VoiceOver, then separately set Dynamic Type to AX3.
- **Steps:**
  1. With VoiceOver, unlock supervisor mode, add a new cell with a word, and save it.
  2. With Dynamic Type at AX3, repeat the same task.
  3. Note whether the passcode entry, editor fields, and save controls are labeled and readable.
- **Expected result:** A caregiver who uses VoiceOver or large text can unlock, edit, and save vocabulary.
- **Pass criterion:** The unlock, add-cell, and save task can be completed with VoiceOver and with Dynamic Type at AX3.
- **Fail criterion:** The task cannot be completed with VoiceOver or at AX3, or any required control is unlabeled or unreadable.
- **Evidence to record:** Screen recordings with audio.
- **Maps to:** WCAG 2.2 4.1.2 Name, Role, Value (Level A); WCAG 2.2 1.4.4 Resize Text (Level AA); WCAG 2.2 3.3.2 Labels or Instructions (Level A).

## 5. Reporting

### Results table format

Every report includes a results table with one row per test, in test ID order:

| Test ID | Result | Severity | Evidence file | Notes |
| --- | --- | --- | --- | --- |
| VO-01 | Fail | Major | VO-01_appname_2.3.1_iPad-10th-gen_iPadOS-26.1_2026-10-21.mov | 6 of 48 cells on the Food page announced image file names. |
| SC-04 | Not Applicable | | | The app has no built-in scanner; iPadOS Switch Control tested under SC-01. |
| EG-01 | Blocked | | | No eye tracker available to the evaluator. |
| EM-01 | Pass | | EM-01_appname_2.3.1_iPad-10th-gen_iPadOS-26.1_2026-10-21.mov | Help button visible on every page; one action from any screen. |

The Severity column is filled only for Fail results.

### Reporting rules

- A report lists **every test** in this protocol version, including tests that were Not Applicable, Blocked, or Not Evaluated. Not Applicable and Blocked rows must include a reason.
- A report states the protocol version, the app name, version, and build, the edition, the device model, the OS version, the test dates, the run type (fresh install or configured state), and the evaluators and their roles.
- A report states whether the evaluator is the vendor, an independent third party, or a purchaser.
- A report never presents a total, percentage, score, or grade. Results are per test.
- A report describes observations. It does not rank or recommend products.
- Reports are submitted through the test result issue template in this repository, or attached to an Accessibility Conformance Report based on [ACR-TEMPLATE.md](ACR-TEMPLATE.md).
- Evidence files should be kept for as long as the report is in use and offered on request. Remove personal information about participants before sharing.

## 6. Change control

- **Versioning.** This protocol uses semantic versioning (MAJOR.MINOR.PATCH). A MAJOR version changes a pass or fail criterion in a way that can change results, or removes a test. A MINOR version adds tests or categories. A PATCH version fixes wording, typos, or links without changing what a test measures.
- **Proposing changes.** Changes go through the protocol change issue template in this repository. Describe the problem, the proposed text, the affected test IDs, and the evidence or standard that supports the change.
- **Stable IDs.** Each test has a stable ID. IDs are never reused. A retired test keeps its ID, is marked "Retired in version X.Y.Z" with a reason, and its number is not assigned to any new test. New tests take the next unused number in their category.
- **Citing a version.** Every report and ACR cites the exact protocol version used. Results from different protocol versions should not be compared without checking the change log.
- **Platform changes.** When an OS update moves a setting or renames a feature, the settings paths are updated in a PATCH release. When an OS update changes what can be tested, the affected tests are reviewed in a MINOR or MAJOR release.

## Appendix A: WCAG 2.2 success criteria referenced

WCAG 2.2 is written for web content. This protocol applies its success criteria to native AAC apps following the approach used by the W3C's guidance on applying WCAG to non-web information and communications technology, and by Section 508 and EN 301 549. Where a criterion is applied by analogy (for example, 3.2.6 Consistent Help applied to the consistent location of emergency vocabulary, or 3.1.1 Language of Page applied to speech language), the test text explains the AAC-specific requirement.

| Criterion | Name | Level | Test IDs |
| --- | --- | --- | --- |
| 1.1.1 | Non-text Content | A | VO-01, VO-10, HC-05 |
| 1.3.1 | Info and Relationships | A | VO-02, VO-09, VO-10 |
| 1.3.2 | Meaningful Sequence | A | VO-03, SC-02 |
| 1.3.3 | Sensory Characteristics | A | HC-06 |
| 1.3.4 | Orientation | AA | DT-03 |
| 1.4.1 | Use of Color | A | HC-04, HC-06 |
| 1.4.2 | Audio Control | A | VO-08, SC-06, EM-05, SP-03, SP-06, SP-08 |
| 1.4.3 | Contrast (Minimum) | AA | HC-01, HC-05 |
| 1.4.4 | Resize Text | AA | DT-01, DT-02, DT-04, DT-05, CC-08 |
| 1.4.6 | Contrast (Enhanced) | AAA | HC-03 |
| 1.4.10 | Reflow | AA | DT-02, DT-03, DT-05 |
| 1.4.11 | Non-text Contrast | AA | SC-07, EG-05, HC-02 |
| 1.4.12 | Text Spacing | AA | DT-02 |
| 2.1.1 | Keyboard | A | VO-07, SC-01, SC-03, SC-08, SC-10, EG-07, EM-03 |
| 2.1.2 | No Keyboard Trap | A | VO-04 |
| 2.2.1 | Timing Adjustable | A | SC-03, SC-04, SC-05, SC-08, EG-04 |
| 2.2.2 | Pause, Stop, Hide | A | SC-05, EG-07, RM-02, SP-03 |
| 2.3.1 | Three Flashes or Below Threshold | A | RM-02 |
| 2.3.3 | Animation from Interactions | AAA | RM-01, RM-03 |
| 2.4.1 | Bypass Blocks | A | VO-09, EM-01, EM-02 |
| 2.4.2 | Page Titled | A | VO-06 |
| 2.4.3 | Focus Order | A | VO-03, VO-04, SC-02 |
| 2.4.6 | Headings and Labels | AA | VO-01, VO-09 |
| 2.4.7 | Focus Visible | AA | SC-07, EG-05, HC-02 |
| 2.4.11 | Focus Not Obscured (Minimum) | AA | DT-03 |
| 2.4.13 | Focus Appearance | AAA | SC-07 |
| 2.5.1 | Pointer Gestures | A | VO-07, EG-01, EG-02, TT-05 |
| 2.5.2 | Pointer Cancellation | A | SC-09, EG-06, TT-04 |
| 2.5.4 | Motion Actuation | A | RM-03 |
| 2.5.5 | Target Size (Enhanced) | AAA | EG-03, TT-01 |
| 2.5.7 | Dragging Movements | AA | TT-05 |
| 2.5.8 | Target Size (Minimum) | AA | EG-03, TT-01, TT-02, TT-03 |
| 3.1.1 | Language of Page | A | SP-01 |
| 3.1.2 | Language of Parts | AA | SP-01 |
| 3.2.1 | On Focus | A | VO-06, SC-11, EG-06, SP-05 |
| 3.2.2 | On Input | A | SP-05 |
| 3.2.3 | Consistent Navigation | AA | SC-10, SC-11 |
| 3.2.6 | Consistent Help | A | SC-10, EM-01, EM-02, EM-03, EM-04, EM-07, CC-04 |
| 3.3.2 | Labels or Instructions | A | EG-02, PR-05, CC-08 |
| 3.3.4 | Error Prevention (Legal, Financial, Data) | AA | EG-08, TT-03, EM-06, SP-04, SP-09, OF-04, PR-08, CC-01, CC-02, CC-03, CC-05 |
| 3.3.8 | Accessible Authentication (Minimum) | AA | OF-03, PR-01 |
| 4.1.2 | Name, Role, Value | A | VO-01, VO-02, VO-05, SC-01, SC-12, EM-02, CC-02, CC-08 |
| 4.1.3 | Status Messages | AA | VO-05, VO-06 |

## Appendix B: Settings paths

These paths are written for current iPadOS and iOS versions. Names and positions can change between OS releases. If a path does not match, open Settings and use the search field to find the feature by name.

| Feature | Settings path | Notes |
| --- | --- | --- |
| VoiceOver | Settings > Accessibility > VoiceOver | Practice gestures in VoiceOver Practice before testing. |
| VoiceOver rotor options | Settings > Accessibility > VoiceOver > Rotor | Confirm Headings is in the rotor for VO-09. |
| Switch Control | Settings > Accessibility > Switch Control | Add switches under Switches before turning Switch Control on. |
| Switch Control timing | Settings > Accessibility > Switch Control > Timing (or similar) | Includes auto scanning time, hold duration, and ignore repeat. |
| Switch Control group items | Settings > Accessibility > Switch Control > Group Items (or similar) | Used for SC-03 with platform scanning. |
| AssistiveTouch and dwell | Settings > Accessibility > Touch > AssistiveTouch | Dwell Control and pointer device options appear here when a pointing device is connected. |
| Eye tracking (platform) | Settings > Accessibility > Physical and Motor section | Available on some devices and OS versions; record whether used. |
| Touch Accommodations | Settings > Accessibility > Touch > Touch Accommodations | Hold Duration, Ignore Repeat, Tap Assistance. |
| Larger Text (Dynamic Type) | Settings > Accessibility > Display and Text Size > Larger Text | Turn on Larger Accessibility Sizes for AX1 to AX5. |
| Bold Text | Settings > Accessibility > Display and Text Size > Bold Text | Optional additional check for DT tests. |
| Increase Contrast | Settings > Accessibility > Display and Text Size > Increase Contrast | Used for HC-03. |
| Smart Invert | Settings > Accessibility > Display and Text Size > Smart Invert | Used for HC-05. |
| Color Filters (grayscale) | Settings > Accessibility > Display and Text Size > Color Filters | Grayscale can be used for HC-04. |
| Dark mode | Settings > Display and Brightness > Appearance | Light and Dark. |
| Reduce Motion | Settings > Accessibility > Motion > Reduce Motion | Used for RM tests. |
| Guided Access | Settings > Accessibility > Guided Access | Set a passcode; start by triple-clicking the side or Home button in the app. |
| Accessibility Shortcut | Settings > Accessibility > Accessibility Shortcut | Triple-click toggles the selected features. |
| Spoken content and voices | Settings > Accessibility > Spoken Content > Voices | Download platform voices for OF-02 if the app uses them. |
| Focus modes | Settings > Focus | Used for SP-08. |
| Airplane Mode | Control Center, or Settings > Airplane Mode | Used for OF and EM-07. |
| Per-app cellular data | Settings > Cellular (or Mobile Data) | Totals only; used for PR-02 when no proxy is available. |
| App privacy permissions | Settings > Privacy and Security | Review camera, microphone, photos, and other permissions for PR-05. |
| Proxy configuration | Settings > Wi-Fi > (network) > Configure Proxy | Used for PR-02 with a network proxy tool. |

## Appendix C: Glossary

| Term | Definition |
| --- | --- |
| AAC | Augmentative and alternative communication. Methods and tools that supplement or replace speech, including symbol-based and text-based communication apps. |
| Access method | The way a person operates a device: direct touch, VoiceOver, one or two switches, eye gaze, head pointing, or a combination. In this protocol, the access method is the test condition. |
| Scanning | An access method in which items are highlighted one at a time or in groups, and the user activates a switch to select the highlighted item. Auto scan advances on a timer; step scan advances on a switch press. |
| Dwell | Selecting an item by holding a pointer, such as an eye gaze point or head pointer, on it for a set time. |
| Auditory scanning | Scanning in which each highlighted item is announced by a cue (a voice or sound), so the user can scan by listening. The cue is usually distinct from the message voice. |
| Message bar | The area of an AAC app that shows the message being built from selected words, usually with a control to speak it. |
| Core vocabulary | A small set of high-frequency words (for example, "I", "want", "go", "stop", "more") that make up most of what people say across situations. |
| Fringe vocabulary | Words specific to a person, topic, or situation (for example, names, places, foods). |
| Edit lock | A setting that prevents vocabulary and settings from being changed without unlocking, usually with a passcode. Also called supervisor mode. |
| Guided Access | A platform feature that keeps the device in a single app and can disable areas of the screen or hardware buttons, controlled by a passcode. |
| Emergency vocabulary | A set of words and phrases for urgent needs, such as "help", "stop", "pain", and "I'm sick". |
| Configured-state run | A test run with the app set up the way the intended user will use it. |
| Fresh install run | A test run on a newly installed app with default settings. |
| Point (pt) | The device-independent unit of measure on iPadOS and iOS. Physical pixels equal points multiplied by the screen scale factor. |
