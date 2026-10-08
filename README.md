# Mobile Application Development - In-Class Activity 08

## Local Storage: Fall Festival Roster

This Flutter app stores a fictional Fall Festival guest roster in a local
SQLite database. It supports adding, editing, deleting, refreshing, and
validating guests on one Material screen.

## Setup and run

From the project root:

```powershell
flutter pub get
flutter run
```

Use an Android device or emulator on Windows. The assignment does not support
the `sqflite` setup on Flutter web or Windows/Linux desktop.

Verified Flutter SDK: Flutter 3.47.4 stable, Dart 3.13.3.
No Android or iOS device/emulator was connected; only Windows, Chrome, and Edge
were detected. The required mobile manual run is therefore **Pending**.

## Dependencies

The existing generated SDK constraint and project settings were retained.
Dependencies were aligned with the assignment:

- `sqflite: ^2.4.1`
- `path_provider: ^2.1.5`
- `path: ^1.9.0`

No supplied `database_helper.txt` or sample `pubspec.yaml` was available in the
workspace or accessible attachment paths. `lib/database_helper.dart` is a
reconstruction of the documented helper API and schema, not a verbatim copy.

## Implementation summary

- `DatabaseHelper.init()` opens `MyDatabase.db` in the application documents
  directory.
- SQLite table `my_table` contains `_id INTEGER PRIMARY KEY`,
  `name TEXT NOT NULL`, and `age INTEGER NOT NULL`.
- The roster screen loads rows and count from `initState()`, displays explicit
  loading, empty, populated, and read-error states, and uses parameterized
  `whereArgs` for ID-based updates and deletes.
- Names are trimmed and must be nonempty. Ages use `int.tryParse()` and must
  be integers from 0 through 130.
- No records are seeded automatically.
- The generated counter app and obsolete dog example were removed.

## Manual verification matrix

These tests require an Android/iOS run and real app-process restart. Results
have not been performed in this workspace, so all evidence-dependent fields
are intentionally marked **Pending**.

| Test ID | Action/input | Expected | Observed rows/count | Pass/fail |
|---|---|---|---|---|
| T1 | Start with zero disposable rows; press Refresh. | Count 0 and `No festival guests yet`. | Pending | Pending |
| T2 | Add River, 21 and River, 34; record generated IDs as A and B. | Distinct generated IDs; count 2. | Pending; A/B pending | Pending |
| T3 | Edit B to 99 and Cancel; edit B again and save 35. | Cancel preserves 34; update affects 1; count 2; A remains 21. | Pending | Pending |
| T4 | Stop the process and relaunch without clearing storage. | Same IDs, names, ages, and count; no reseeding. | Pending | Pending |
| T5 | Cancel deletion of A, then confirm deletion of A and Refresh. | Cancel leaves count 2; delete affects 1; only B remains; count 1. | Pending | Pending |
| T6a | Blank/space-only name with age 21. | Field-level validation; no write. | Pending; count pending | Pending |
| T6b | Name Maple with age `abc`. | Field-level validation; no write. | Pending | Pending |
| T6c | Name Maple with age `1.5`. | Field-level validation; no write. | Pending | Pending |
| T6d | Name Maple with age `-1`. | Field-level validation; no write. | Pending | Pending |
| T6e | Name Maple with age `131`. | Field-level validation; no write. | Pending | Pending |
| T6f | Add Acorn, age 0. | Accepted; distinct generated ID. | Pending | Pending |
| T6g | Add Oak, age 130. | Accepted; distinct generated ID; final count 3. | Pending | Pending |

Before T4, record the reflection-1 prediction immediately before stopping the
app. Do not substitute a generic prediction after the fact.

## Evidence

Required screenshots are not available yet and must be captured during the
manual Android/iOS run:

- `evidence/T4_before.png` — roster before stopping the app.
- `evidence/T4_after.png` — same roster after force-stop and relaunch.
- `evidence/T6_invalid.png` — one rejected validation attempt.

For Android T4: stop debugging, open this app's system App info, choose
**Force stop**, and reopen the app from its launcher icon. Do not clear storage
or uninstall. Hot reload, hot restart, and backgrounding alone do not qualify.

## Analyzer and unresolved issues

The final analyzer output is saved in `evidence/analysis_output.txt`.
Device-only manual tests and the Flutter target/device version remain
**Pending** until run locally. No source archive was created because the
instructor's submission/archive instructions were not included in the supplied
material.

## Graduate reflections

The following are intentionally deferred:

1. Reflection question 1: **Deferred - to be completed by the student.**
2. Reflection question 2: **Deferred - to be completed by the student.**
3. Reflection question 3: **Deferred - to be completed by the student.**
4. Reflection question 4: **Deferred - to be completed by the student.**

The supplied assignment omitted the detailed text for questions 2-4 and the
submission/rubric sections; no additional instructions are invented here.

## AI assistance disclosure

Adapt this statement to the course policy and your actual use:

> I used an AI assistant to help restructure the starter Flutter project,
> implement the documented SQLite CRUD UI, and review static-analysis output.
> I inspected, ran, and will personally verify the resulting app and record
> my own manual observations and reflections.

## Proposed source ZIP checklist

Because the instructor's exact archive format was not supplied, verify with
the course instructions before submitting. A proposed checklist is:

- Include `lib/`, `pubspec.yaml`, `pubspec.lock`, platform project files, and
  this README.
- Include final `evidence/analysis_output.txt` and the three screenshots once
  captured.
- Exclude build caches such as `.dart_tool/`, `build/`, and IDE metadata unless
  the instructor explicitly requests them.
