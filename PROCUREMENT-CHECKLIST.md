# AAC Procurement Checklist for School Districts

Use this checklist when evaluating an augmentative and alternative communication (AAC) app for students. It is based on the [AAC Accessibility Test Protocol](PROTOCOL.md) and asks for evidence gathered on real hardware with the access methods your students actually use.

## Accessibility

- [ ] Request an Accessibility Conformance Report (ACR) based on the [ACR template](ACR-TEMPLATE.md) and this protocol, citing the protocol version used.
- [ ] Require hardware test evidence (device model, OS version, test date) for every "Supports" claim; do not accept simulator results.
- [ ] Confirm VoiceOver results (VO tests) for any student who is blind or has low vision.
- [ ] Confirm Switch Control and in-app scanning results (SC tests) for any student who uses switches, including auditory scanning if needed.
- [ ] Confirm eye gaze and dwell results (EG tests) with the class of eye tracker the student will use.
- [ ] Confirm every control used during communication is at least 44 x 44 pt (TT-01), with larger cells available.
- [ ] Confirm Dynamic Type support to AX5 without truncated words (DT-01, DT-02).
- [ ] Confirm Reduce Motion and contrast settings are honored (RM, HC tests).
- [ ] Confirm the vendor's documentation lists supported access methods and compatible assistive technology.
- [ ] Trial the app with the specific students, with their access methods, before purchase.

## Privacy and student data

- [ ] A data processing or student data privacy agreement is signed before any student uses the app (PR-10).
- [ ] The vendor states its position on FERPA, COPPA, and your state's student privacy laws in writing (PR-09). Consult district counsel.
- [ ] No advertising and no third-party analytics in the student edition, or every third-party service is disclosed (PR-06).
- [ ] Network traffic was checked against the privacy policy and App Store privacy label (PR-02).
- [ ] Data at rest, message history storage, and backup behavior are documented, and message history can be turned off (PR-03).
- [ ] Message history, user data, and accounts can be deleted on request, with a documented retention period (PR-04).
- [ ] Cloud sync is opt-in (PR-07), and camera and microphone are requested only when needed (PR-05).
- [ ] The contract states that the student and family own the student's vocabulary and communication data.

## Offline

- [ ] Full vocabulary and speech work in Airplane Mode (OF-01).
- [ ] Voices are downloaded to the device and work offline (OF-02).
- [ ] No login, subscription, or license wall blocks communication offline (OF-03).
- [ ] The app launches and speaks offline after a device restart (OF-05).

## Safety

- [ ] Emergency vocabulary (help, stop, pain) is reachable in at most two actions from any screen (EM-01).
- [ ] Emergency vocabulary is reachable under every access method the student uses (EM-02, EM-03).
- [ ] An edit lock protects vocabulary and cannot be bypassed with the student's access method (CC-01 to CC-03).
- [ ] The app works with Guided Access, and emergency vocabulary still works in Guided Access and in any student mode (EM-04).
- [ ] Speech is audible with the Silent switch or a Focus mode on, or the behavior is documented (SP-08).
- [ ] Emergency vocabulary cannot be hidden or deleted without supervisor access (EM-06).

## Support

- [ ] The vendor states a support response time in writing, including for communication-blocking defects.
- [ ] Training is available for staff and for families, in accessible formats.
- [ ] A named accessibility contact is provided.
- [ ] The vendor explains how accessibility bugs are reported, tracked, and communicated back to the district.
- [ ] Accessibility fixes are included in the license at no extra cost.
- [ ] Support channels are accessible to AAC users and people with disabilities.

## Exit and data export

- [ ] Vocabulary can be exported in an open, documented format such as CSV or JSON (CC-06).
- [ ] Vocabulary can be backed up to a file the family or district controls and restored (CC-05).
- [ ] The vendor describes how a student's vocabulary can move to another app.
- [ ] Account deletion is available from inside the app (PR-04).
- [ ] The contract sets an end-of-contract timeline for data return and deletion.
- [ ] Core communication keeps working if a subscription lapses, or the behavior is documented in the contract.

## Pricing and licensing

- [ ] Pricing model is clear: per device, per student, or site license.
- [ ] License terms allow the app to follow the student between devices, classrooms, and home.
- [ ] A trial on real student hardware, with real access methods, is available before purchase.
- [ ] Costs for voices, symbol sets, eye gaze support, or scanning features are listed separately if they are add-ons.

## Questions to ask the vendor

1. Can you provide an ACR based on the AAC Accessibility Test Protocol, with hardware test evidence for every "Supports" claim?
2. Which access methods (VoiceOver, Switch Control, your own scanner, eye gaze) did you test on physical hardware, and on which devices and OS versions?
3. What data leaves the device, to which hosts, and why? Will you sign our student data privacy agreement?
4. How does a student reach "help" or "stop" from any screen with a switch or eye gaze, and can anyone hide those words?
5. What happens to communication if the device is offline, or our subscription ends?
6. How do we export a student's vocabulary in an open format if the student moves to another app?
7. How do we report an accessibility bug, and how quickly is a communication-blocking defect fixed?

This checklist is part of the AAC Accessibility Test Protocol by Dr. Jeffrey Davis, PhD, ATP, licensed under CC BY 4.0 (see [LICENSE](LICENSE)).
