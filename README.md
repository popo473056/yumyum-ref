# YumYum (냠냠이): MVP result

Midterm MVP submission for KMU AI에이전트실무 2026.

| | |
|---|---|
| Name | 박준혁 (Park Junhyeok) |
| Class section (분반) | 3학기 |
| Service | 냠냠이 (YumYum), an iPhone app for cooking Korean food in English |
| Demo video (1 min) | https://drive.google.com/file/d/1yIAQTaCCPLN8-uF-fGDIpBfJZtncOKxi/view?usp=sharing |
| App (live) | https://apps.apple.com/us/app/yumyume/id6829632671 (US App Store, free, released 2026-11-03) |
| Site, privacy policy, photo credits | https://popo473056.github.io/yumyum-app/ |
| Slides | [`slides/yumyum-mvp-result.html`](slides/yumyum-mvp-result.html) (22 slides, the file submitted to the classroom) |

## What this repository contains, and what it leaves out

This repository is a public reference for the midterm review. It holds the slides, the demo link, the verification evidence, and the agent work log.

The app source code is not in this repository and is not public. The author decided to keep it private. The app ships as a binary through the US App Store, so you can run it without the source.

| Public here | Private (not in this repository) |
|---|---|
| Slides with the embedded 1-minute demo video | Flutter app source, native iOS adapter, tests |
| Demo video link | Recipe, glossary, and voice-guide content files |
| Verification results with the commands, outputs, and dates | Raw test logs, device QA scripts, build signing material |
| Agent work log: requests, human checks and fixes, blockers and recovery | Development history (commits, design files, internal docs) |

Because the source stays private, you cannot rebuild the app from this repository. The commands and file paths cited below refer to the private repository so that the evidence stays traceable. This repository contains no keys, tokens, or personal data of other people.

## Rubric map

| Rubric item | Where to find it |
|---|---|
| 1. 동작하는 MVP | [Demo](#demo), [How to run](#how-to-run) |
| 2. 기획안과의 차이 | [Changes from the proposal](#changes-from-the-proposal) |
| 3. 검증 결과 | [Verification](#verification) |
| 4. 공개와 재현 | This README, [`LICENSE`](LICENSE), [`.gitignore`](.gitignore), [`.env.example`](.env.example), [What this repository contains](#what-this-repository-contains-and-what-it-leaves-out) |
| 5. 에이전트 작업 기록 | [Agent work log](#agent-work-log) |

## Problem

Picture an English speaker who cannot read Korean and wants to cook doenjang-jjigae for the first time. Three things get in the way:

1. Picking a dish: Korean dish names are hard to read.
2. Reading ingredients: they do not know what doenjang is or what to use instead.
3. Cooking: wet hands make touching the screen awkward, and they lose track of time.

YumYum answers each one. Every dish shows its Hangul name large with the official romanization below it. Tapping an ingredient opens a glossary entry with the Hangul name, a plain English description, and substitutes. While cooking, you say "Next" to move a step, the app reads each step aloud in English, and timers start on their own.

This problem statement is a hypothesis. No target user has tested it yet (see V1 and V2 below).

## Demo

- Video, 1 minute: https://drive.google.com/file/d/1yIAQTaCCPLN8-uF-fGDIpBfJZtncOKxi/view?usp=sharing
- The same video is embedded in slide 6 of [`slides/yumyum-mvp-result.html`](slides/yumyum-mvp-result.html).
- Chapters: 0:00 intro, 0:07 choosing a dish, 0:15 ingredient glossary, 0:26 step guide, 0:37 automatic timer, 0:50 finished dish.

The video is an edited simulator recording. The timer wait is cut, and the Korean narration is synthetic speech (Qwen3-TTS, preset voice) added for the intro. It is not a recording of the app's own voice guide or alarm sound. Verification 3 covers voice commands on a real iPhone.

## How to run

1. Use the app: on an iPhone with a US App Store account, install YumYum from https://apps.apple.com/us/app/yumyume/id6829632671 . It needs no login and no network after install. The app is listed only in the US storefront; without a US account, steps 2 and 3 show the same flows.
2. Watch the demo: open the Google Drive link above. Anyone with the link can view it.
3. Open the slides: download [`slides/yumyum-mvp-result.html`](slides/yumyum-mvp-result.html) and open it in a desktop browser. Use the right and left arrow keys or the on-screen buttons. The file is self-contained (6.4 MB) and loads nothing from the network.

No environment variables or secrets are needed for any of these steps. [`.env.example`](.env.example) says so.

## What the MVP does

- 55 Korean recipes with 290 cooking steps, 143 of them with timers, and 400 English voice-guide clips.
- Ingredient glossary: Hangul name, plain English description, substitutes.
- Step timer that starts by itself, survives moving between steps, and plays an alarm when it ends.
- English voice commands (72 phrases mapped to 11 actions), parsed on the device by a fixed dictionary. The app calls no LLM and no server at run time.
- No account, no ads, no data collection. The App Store listing declares "Data Not Collected".

## Changes from the proposal

The proposal dates from 2026-10-23. The released version dates from 2026-11-03.

| Proposal | Actual | Reason |
|---|---|---|
| Build from scratch in one week | Converted a Korean voice cooking app, in progress since September, to English on 2026-10-27 | Reusing the cooking-session logic, screens, and tests left time for recipes and timers |
| 3 recipes, 5 if time allows | 5 in the MVP build, 55 in the release | After the 5-recipe build passed its tests, the author widened the scope. Five writer agents and one reviewer agent added 50 recipes |
| No voice commands or English narration in scope | Off in the MVP build, on in the release build through the `YUM_EXTRAS=true` build flag | Kept the MVP scope without deleting code. Turned on for release after the 2026-10-29 device test |
| App Store submission out of scope | Submitted 2026-11-02, released in the US on 2026-11-03 | The author moved the release date forward |
| Dish images undecided (code-drawn illustrations in the MVP) | 46 photos from Wikimedia Commons, redrawn; 9 bowl illustrations | Photos make dishes easier to recognize. Only CC0, CC BY, and CC BY-SA sources; no Pinterest images |
| Hermes writes the code | Claude Code agents wrote the code and ran this submission through the classroom agent API | Kept the existing development setup, repository rules, and checklist |
| Demo recorded on an iPhone | One-minute simulator edit with Korean narration, linked from Google Drive | A device recording with sound is not done yet. Voice was checked in a separate device test |
| Three testers use the app (V1, V2) | Zero testers so far | Recruiting has not happened yet. The pass criteria stay as written |

Unchanged: no revenue features, no LLM calls while the app runs, no server, no login.

## Verification

Six checks, each with the command or source, the result, and the date.

| # | Check | Command or source | Result | Date and conditions |
|---|---|---|---|---|
| 1 | Automated tests and static analysis | `flutter test`, `flutter analyze` | `+331 ~42: All tests passed!` and `No issues found!` The 42 skipped tests need a local server or are golden-image tests that the default run skips | 2026-11-02; rerun 2026-11-06 on commit `371f660` with the same result |
| 2 | Recipe and audio bundle check | `test/release/seed_bundle_test.dart`, `test/core/glossary_coverage_test.dart` | All 55 recipes parse; all 400 voice clips match size and SHA-256; every glossary entry has a Hangul name and an English description | Same runs as check 1 |
| 3 | Voice commands on a real iPhone | `integration_test/device_voice_test.dart`, `tool/device_voice_qa.py` | 45 of 54 recognized (83%). Before a threshold fix: 31 of 38 (82%) | 2026-10-29, iPhone 15, one synthetic voice played from a Mac speaker. The two runs differ in count and audio path, so they are not a controlled comparison |
| 4 | Touch flow from choosing a dish to finishing | `integration_test/journeys_test.dart`, `demo_test.dart`, `promo_demo_test.dart` | 13 of 13 scenarios pass (8 min 9 s). Demo flow also passes on an iPhone 15 | 2026-10-28, 2026-11-02 |
| 5 | Voice-guide clipping and repetition | `tool/build_seed.dart`, Whisper `small.en` transcription | 31 clips (30 recipe clips and 1 intro) show 0 truncations and 0 repeats. Loudness normalized: before -27.3 to -21.5 LUFS, after -17.7 to -15.9 LUFS | 2026-10-29. The other 370 clips and a human listening pass are not done |
| 6 | Upload, review, release | `flutter build ipa --export-method app-store --dart-define=YUM_EXTRAS=true`, `xcrun altool --upload-app`, App Store Connect API | Build processing `VALID`; submitted for review 2026-11-02 15:36 KST; status `READY_FOR_SALE` | 2026-11-02 to 2026-11-03. Public evidence: the App Store link above |

The 9 voice-command misses: 3 with no result (slower, faster, done), 2 "stop cooking" heard as "Start cooking", 2 "back" heard as "Bad", 1 "next" heard as "No", and 1 "go back" recognized at confidence 0.21 and ignored. Kitchen noise and other voices are untested.

### Proposal checks still open

Checks 1 to 6 show that the app works and shipped. They do not replace the user checks from the proposal.

| Proposal check | Pass criterion | Status |
|---|---|---|
| V1: finish a recipe with English guidance only | 3 of 3 testers reach the completion screen | Not run. 0 testers |
| V2: understand unknown ingredients through the glossary | 0 missing glossary entries; at least 80% "now I know" answers | Partly done. The glossary coverage test passes; tester understanding is untested |
| V3: timer alarm | 10 runs on an iPhone, each within ±2 s, 5 of them with the screen off | Partly done. Alarm playback and the end screen checked on an iPhone 15; the 10-run timing test is not done |

## Agent work log

### What the agents did

- Main session (Claude Opus): split the work, drafted designs, merged results.
- Workers (mostly Claude Sonnet): code, recipe drafts, image processing, documents.
- Reviewers (read-only, separate sessions): checked results and evidence for gaps and errors.

| Date | Request |
|---|---|
| 09-02 to 09-05 | Design docs, build checklist, and Figma design system for a hands-free Korean cooking app |
| 09-03 | First version built by an agent team (29 commits in one day) |
| 10-10 | App Store readiness review (4 inspectors, 1 worker, 1 reviewer) |
| 10-23 | Midterm proposal draft, scored by 3 grading agents |
| 10-27 | Conversion to English (6 workers, 1 reviewer): 5 recipes, glossary, step timer |
| 10-28 | Rubric cross-check, demo recording, turning off features outside the proposal |
| 10-29 | Sound and voice-command QA on an iPhone 15 |
| 10-30 to 11-01 | Button rules, mascot poses, conversational cooking screen, photo rules, new Figma file |
| 11-02 | 50 more recipes (5 writers, 1 reviewer, 2 photo workers), App Store Connect entry, build upload, review submission |
| 11-03 | Release confirmed; download links added to the slides and site |
| 11-06 | Slides finalized; this repository published; result submitted through the classroom agent API |

Every session read the repository rules (`AGENTS.md`) and the build checklist first. One rule held throughout: no item is marked done until its pass condition is checked. 183 commits over 18 working days (09-02 to 11-03).

### What the author checked or fixed

- Scope: adjusted the proposal scope, and on 10-28 chose to switch off out-of-scope features instead of deleting them.
- Device: on 10-29 cooked the rolled-omelette recipe by voice. Yes, Next, Repeat, and Go back all worked (quiet room, one speaker).
- Screens: asked for one button size across the app, had the cooking screen revised twice, adjusted headings and spacing in Figma.
- Rights: set the photo source and license rules and the recipe credit line. All 55 recipes stay at `rightsStatus: pending`; the human content review is not done.
- Accounts: accepted the Apple developer terms and filled in the privacy answers. On the author's request, an agent submitted the build for review through the API.

### Where it got stuck and how it recovered

| Problem | Recovery |
|---|---|
| Two workers read files for 20 to 40 minutes and wrote nothing (09-03) | Stopped them; the main session wrote the code. New rule: no output file in 15 minutes means one status check, then stop |
| An agent recorded `rightsStatus: approved` and a review date without any review | A reviewer caught it; status restored to unapproved. Only checked results get recorded |
| Correctly recognized commands fell below the 0.5 confidence threshold (0.39 to 0.42) and did nothing (10-29) | Threshold lowered to 0.3 only when the text matches the dictionary exactly; command phrases passed to the recognizer as hints |
| On a fresh install, the permission prompt and mic start overlapped; after "Allow" the app stayed at "You can cook without the mic" | Permission rechecked on the allow event and on app resume (commit `151643c`, 2 widget tests) |
| Qwen3-TTS repeated one sentence without end and used 38 GB of memory (10-27) | Capped generation length; on failure, retry with a new random seed |
| A test build left on the iPhone kept advancing screens by itself (10-30) | New rule: reinstall the normal development build after every device test |
| After an account move, agents could not open the original Figma file | Built a new Figma file and recreated the 24 implemented screens (10-30) |
| App Store export failed with `PLA Update available` | The account owner accepted the updated agreement; rerun gave `VALID` (11-02) |

## Plan to the final

| Priority | Item |
|---|---|
| Done | App Store review passed; US release on 2026-11-03 |
| 1 | V1 and V2 with 3 testers who cannot read Korean |
| Open | V3: 10 timer runs on an iPhone, 5 with the screen off, each within ±2 s |
| Open | Human review of cooking and safety text in all 55 recipes; listening check and rights check for the voice clips |
| Open | Device demo recording with the app's voice and alarm sound |
| Later | Review 50 more planned recipes after the checks above |

Release form and place: iPhone app on the US App Store, free, with the site at https://popo473056.github.io/yumyum-app/ .

Source: the app source stays private. This repository is the public record for the course.

## License

See [`LICENSE`](LICENSE). The slides and this README belong to the author. Third-party material inside the slides keeps its own license: food photos adapted from Wikimedia Commons (CC0, CC BY, CC BY-SA; per-image credits at https://popo473056.github.io/yumyum-app/credits.html) and the Gowun Dodum font (SIL Open Font License 1.1).
