## 26512 beta

### Changelog
- Fixed playhead lagging behind trigs
- Fixed LIVE REC mode not respecting track loop length, speed and wrap
- Fixed FUNC+PAGE not opening TRACK SETUP window while in LIVE REC mode
- Added FUNC+CLEAR/COPY/PASTE/UNDO to PATTERN SETUP window
- Added UNDO to actions that affect TRACK SETUP params
- CLEAR PATTERN now clears TRACK SETUP and PATTERN SETUP params
- Fixed new SysEx command IDs colliding with stock status commands. It was necessary to move some of the new SysEx commands:
```
Updated commands:

Track select:           F0 00 20 3C 03 00 66 <idx> F7

Dump current global:    F0 00 20 3C 03 00 62 00 F7
Dump global:            F0 00 20 3C 03 00 62 01 <idx> F7
Dump global range:      F0 00 20 3C 03 00 62 02 <idx> <bank> F7
Restore global:         F0 00 20 3C 03 00 63 <idx> 01 <data> F7
```

## 26510 beta

### Changelog
- Added TRIG CONDITIONS (L1, L2, !L2, L3, !L3, L4, !L4, 1S, !1S, P1, P2, P5, P7, P9) + new menu options & shortcuts for copy/paste/clear (details below)
- Added per-track LOOP LENGTH and SPEED settings + new menu options & shortcuts for copy/paste/clear (details below)
- Added new SPEED options (1/2x, 1/4x, 1/8x)
- Added WRAP AFTER and CHAIN AFTER settings
- Added GLOBAL > SEQ > PATTERN SETUP (MIDISEQ category renamed to SEQ)
- Removed SONG slots 13-24 to make space for new data
- Added new SysEx commands for requesting the extended data stored in the region previously used for SONG slots 13-24 (dumps can also be accepted back in via SYSEX RECV)
- Added new SysEx command for changing currently selected track:
    `F0 00 20 3C 03 00 72 <idx> F7`
    (00..05 = synth tracks 1-6, 06..0B = MIDI tracks 1-6)
- Added value indicator when adjusting LEV
- Added quick kit reload shortcut: FUNC + TEMPO (TAP TEMPO remapped to TEMPO + TEMPO)
- Added 'CTL AL' esque feature where you can control a parameter across all tracks relatively, with FUNC + A-H (this currently does not include the first 5 LFO params or MIDI track params)
- Track LEDs now blink on trigs during playback
- Added pattern-start SysEx event: `F0 00 20 3C 03 00 73 <pattern_idx> F7`
- Attempted to fix a rare bug where a track's pitch gets stuck higher than it should be after a pattern change, possibly due to a stale transpose value
- Removed animated boot splash
- Inherits additions from MNMX X.01A firmware, including the kit workspace SysEx command and CC out on track muting

#### TRIG CONDITIONS
- Conditions are accessible by holding a trig, found to the right of the base note of a trig, beneath the piano UI in the bottom left. The condition can then be changed by turning LEV.
- L1 is default and acts the same as a normal trig.
- L2 means play only on the second instance (e.g. 2, 4, 6, etc.), whereas !L2 means don't play on the second instance (e.g. 1, 3, 5, etc.) L3, !L3, L4 and !L4 follow suit.
- 1S means 'oneshot' - play once and never again. !1S is the opposite - don't play once, then always play.
- P1 = 10% chance to play, P2 = 20%, P5 = 50%, P7 = 70%, P9 = 90%.
- L-type conditions and oneshots are reset on STOP > PLAY or pattern changes.
- Conditions can be cleared per-track via FUNC + CLEAR (hold) and selecting COND.
- Conditions on a particular trig can be cleared with TRIG + FUNC + CLEAR. Clearing param locks remains accessible with TRIG + CLEAR.
- Removing a trig clears its condition.
- COPY MELODY action also includes trig condition data.

#### PER-TRACK LOOP LENGTH & SPEED
- The SCALE SETUP menu is now split into the PATTERN SETUP or TRACK SETUP menu.
- The PATTERN SETUP menu is accessible while REC is off, and the TRACK SETUP menu is accessible while REC is on.
- In TRACK SETUP, you can set the currently selected track's loop length anywhere from 2 steps to 64 steps, and set the track's speed (1x, 3/4x, 3/2x, 2x), including new slower speeds (1/2x, 1/4x, 1/8x).
- In PATTERN SETUP, you will find WRAP AFTER and CHAIN AFTER.
- WRAP AFTER controls after how many steps track loops are reset back to step 1. It can be set to anywhere from 2 steps to 1024 steps, to INF steps (no wrapping), 'TRACK' (wrap at the end of the longest track's loop, factoring in speed too), and 'GLOBAL' (use the GLOBAL PATTERN SETUP's WRAP AFTER setting - accessible via GLOBAL > SEQ > PATTERN SETUP). You can quickly move through these values with FUNC + LEV.
- CHAIN AFTER controls at what interval the currently playing pattern is permitted to transition to another pattern. For example, if you set CHAIN AFTER to 16 steps, pressed play, and then queued up a pattern change - the transition to that pattern would occur at the next 16 step interval. You can set CHAIN AFTER anywhere from 2 to 64 steps, as well as 'TRACK' (transition at intervals equal to the length of the longest track's loop, factoring in its speed too), and 'GLOBAL' (use the GLOBAL PATTERN SETUP's CHAIN AFTER setting - accessible via GLOBAL > SEQ > PATTERN SETUP).
- On first initialisation/migration, untouched pattern track lengths are seeded from the pattern's existing stock scale length, and speed follows the stock pattern speed.
- While the TRACK SETUP window is open, PAGE + COPY / PASTE can copy TRACK loop settings to other tracks. PAGE + CLEAR resets the track to 16/16, 1x.
- While the PATTERN SETUP window is open, pasting track settings (PAGE + PASTE) will apply those settings to all tracks at once. PAGE + CLEAR will clear all track settings.
- By default, WRAP AFTER and CHAIN AFTER are both set to GLOBAL, and the global WRAP AFTER and CHAIN AFTER are set to INF and TRACK respectively.

#### SYSEX BACKUPS
- To maintain compatibility with stock pattern & kit backups, the extended data is backed up & restored as separate messages, using separate SysEx commands. You can make dump requests for this data using the following new SysEx commands:

```
Ext data commands:

Dump current pattern:   F0 00 20 3C 03 00 6E 00 F7
Dump pattern:           F0 00 20 3C 03 00 6E 01 <idx> F7
Dump pattern range:     F0 00 20 3C 03 00 6E 02 <idx> <idx> F7
Restore pattern:        F0 00 20 3C 03 00 6F <idx> 01 <bytes> F7

Dump current global:    F0 00 20 3C 03 00 70 00 F7
Dump global:            F0 00 20 3C 03 00 70 01 <idx> F7
Dump global range:      F0 00 20 3C 03 00 70 02 <idx> <bank> F7
Restore global:         F0 00 20 3C 03 00 71 <idx> 01 <data> F7
```

The new firmware can also restore ext data backups via SYSEX RECV as you would other backups, but is not yet included in SYSEX SEND > ALL, PAT+KIT, SONG+P+K, etc.
