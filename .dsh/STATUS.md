# Ukrainian Localization — COMPLETE

## Result
- `Natives/resources/uk.lproj/Localizable.strings` — fully translated (1977 lines, 1975 keys).
  - 1936/1975 values contain Cyrillic; the remaining 39 are legitimate Latin tokens
    (OK, Minecraft, Xbox/PlayStation buttons A/B/X/Y/L1–R3, OpenGL/Zink/ANGLE, TouchController,
    regex keys i18n_str_641/642/643, empty commented footers).
- `Natives/resources/uk.lproj/InfoPlist.strings` — both permission descriptions translated,
  keys byte-identical to en.lproj.

## Verification (byte-level, vs en.lproj ground truth)
- Placeholder parity: every key's `%` byte count matches en exactly (0 mismatches).
- `\n` escape parity: 0 mismatches.
- Positional specs (`%N$@/%N$ld/...`): 0 invalid (fixed several `%2$файлів`-type bugs).
- Quote balance: every line has balanced unescaped `"` (0 issues; fixed 2 truncated values:
  preference.detail.mod_touch_enable, i18n_str_222).
- Key parity: uk has all 1973 en keys + 2 legacy keys (preference.title/java_home +
  .detail) that other locales (ru, fr, ko...) also retain — harmless.
- Fixed during audit: i18n_str_196/200/201/956 dropped placeholders; i18n_str_881/222
  truncations; profile.error.name_exists empty value; i18n_str_1300/1302/1304/1305,
  resman.common.import_result, resman.mods.update.done_message, download.progress.file_count_short
  positional bugs; custom_controls.button_edit.stroke_width stray `%`.

## Scratch files
All translation intermediates (ukz_/uko_/ukuo_/ukout_/ukd_/PROMPT_*/etc.) merged and deleted.

## 2026-09-11 Session 2 (forge fixes + CI green)
- Point 1 (stale forge re-download): extractAllMavenEntries + downloadMissingLibraries now size-aware skip (zero-byte/truncated -> re-fetch). Commit ce7ee357.
- Point 2 (method-1 OOM ~80% install crash): per-iteration @autoreleasepool in both install loops -> autoreleased NSData drained per entry, jetsam threshold no longer hit. Commit 26108fb7.
- CI was RED from 3477e8dc mangle wave: glued __weak/__strong typeof (ModLoaderInstallViewController, 3b5e5788) + invalid @localize prefixes (LauncherPreferencesViewController, 2da16d28).
- CI GREEN @ 2da16d2. Pushed to clawz1NIN/mijavios main.
- Remaining: ru batches 16-18, points 4-7 audit.
