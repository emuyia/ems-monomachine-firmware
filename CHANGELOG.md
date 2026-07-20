## 26719 beta

### Changelog

- Fixed pasting MELODY to MIDI track causing pages 3 and 4 to fill with trigs (26711-beta regression)
- Fixed switching POLY mode on/off during playback causing audio to stop (26711-beta regression)
- Fixed note tails of previously selected POLY tracks switching their synth/machine source to the newly selected POLY track, where they should retain their own (26711-beta regression)
- Fixed track LED sometimes staying off when clearing a pattern
- Fixed issue where adjusting track setup or pattern setup values with LEV after previously using LEV for something else would cause the value to change in the opposite direction for one step
- Fixed pattern setup parameter values not updating on pattern changes
- Fixed issue where adjusting pattern setup parameters would become stuck in one direction after a pattern change
- Fixed incorrect playhead position after disabling SONG mode, or after transitioning to a row
- Fixed playhead reaching one step past the OF/LN range in SONG mode while track is set to 2x or 3/2x speed
- Fixed the UNDO actions for both NOTE LOCKS and TRIG COND being armed by clearing one of either
- Fixed PASTE>UNDO NOTE not undoing the trig condition
- 'PATTERN STP' has been changed to 'PTTRN SETUP'
- You can now set audio routing while in POLY mode
- Navigation between columns in expanded super menus is now done with left/right arrow
- LEV value preview is now permanently displayed while in SONG mode
- Various optimisations across the board (will likely introduce regressions)

## 26711 beta

### Changelog

- CONTROL ALL now works with the LEV parameter
- SPP now respects per-track loop lengths, speeds, and WRAP AFTER setting, including in SONG mode
- Fixed not being able to edit trig conditions while in STEP REC (mode 1)
- Fixed transpose not applying on a pasted track or pasted melody during playback
- Fixed FUNC+LEFT/RIGHT not shifting condition data with trigs
- Fixed SysEx track selection not refreshing source track in POLY mode
- Fixed stock bug where notes in POLY mode get stuck after various actions (changing track, pattern, etc.)
- Fixed stock bug where PASTE>UNDO TRANSPOSE does not work
- Fixed stock bug where muting a track that is being triggered by another track, and then unmuting it, causes trigs that were muted during that time to remain muted later
- Fixed stock bug where muting a track that is being triggered by another track would not mute its active ARP sequence
- Fixed stock bug where the playhead is not shown for the initial step triggered by SPP
- Fixed LIVE REC mode not respecting track loop length, speed and wrap when inputting from external MIDI, or when CONTROL OUT 1 > KEYBOARD is set to INT
- Fixed FUNC+LEFT/RIGHT sometimes resurrecting deleted/off-length trigs after reboot or pattern load when shifting tracks with loop lengths longer than 16 steps
- Fixed UNDO PATTERN not restoring track & pattern setup values consistently
- Fixed LEV value preview appearing in SWING SETUP
- Fixed stock SONG MODE row-loop trick regression, so that selected row OF/LN loops continue after returning to pattern mode
- Fixed hidden stock SCALE speed sometimes causing tracks set to 1x to double-trigger
- Fixed POLY mode track LED blinking not working when using internal or external keyboard
- Fixed POLY mode current track LED always blinking despite not being allocated a voice
- Fixed off-length locks blinking on the trig LEDs after shortening a track
- Cleaned up unused ext data migration code

## 26531 beta

### Changelog

#### TRIG CONDITIONS

- Major alterations to the TRIG CONDITIONS feature:
  - To save SRAM space for future features, there is now a maximum of 64 trig conditions allowed per pattern
  - Added TRACK CONDITION option to the TRACK SETUP menu. This lets you set a default condition for all of the trigs on a track to follow
  - Only trig conditions that differ from the TRACK CONDITION value contribute to the maximum 64
  - There is now an indicator to show when a trig condition differs from the default. This is in the form of an inverted box around the value
  - Due to the newly imposed 64 maximum trig conditions, ****upgrading to this beta WILL destroy any conditions that are past the 64 max, for each pattern currently loaded on the device****.
  - Existing condition data is migrated on boot, snapshot load, and SysEx receive. During migration, conditions are kept only up to the new 64 condition limit. As always, if any data is critical, make sure to back it up first.
- Added TRIG + (click) LEV to clear a trig condition
- Fixed CONDITION data not sticking on trigless trigs, note off, FILTER or LFO trigs
- Fixed Lx / !Lx and one-shot trig conditions breaking when WRAP AFTER = INF
- Fixed Lx / !Lx and one-shot trig conditions using stale or incorrect cycle state in some cases
- Fixed multi trig TRIG POS not respecting trig conditions
- Fixed trig conditions on step 1 not applying directly after pattern change

#### TRACK / PATTERN SETUP

- Entering or exiting EDIT mode (REC) now closes the PATTERN SETUP or TRACK SETUP window if present
- Fixed PATTERN SETUP window blocking viewing trig LEDs, page LEDs, and playing notes
- Tweaked PATTERN SETUP window appearance and controls (swapped arrow left/right with up/down)
- Fixed UNDO TRACK SETUP actions not working after you release PAGE
- Changing track speed mid-playback now waits until the next step before applying
- Navigating to another track should no longer put you on an invalid page if that track has a shorter length

#### LIVE REC / STEP REC

- Fixed appearance of the trig LEDs at 1/2x speed or below while LIVE REC is active
- Fixed STEP REC (Mode 1) not opening TRACK SETUP window on FUNC+PAGE
- Fixed STEP REC trig placement not adhering to track speed
- Fixed not being able to use TRIG buttons to set the STEP REC playhead position beyond the first page
- Fixed STEP REC LEDs showing false yellow trigs on pages 2+
- Fixed STEP REC playhead falling outside of track length when switching from a longer track to a shorter track (resolves by clamping)

#### COPY / PASTE / CLEAR / UNDO

- Fixed playback restarting after pasting a track, pattern, track setup or pattern setup
- Fixed PAGE + PASTE/CLEAR not having UNDO actions
- Fixed wide box on super COPY/PASTE menu despite no additional options
- Fixed super COPY/PASTE/CLEAR/UNDO menu being accessible while the PATTERN SETUP window is open. This also fixes the '(...) PATTERN' message from showing briefly when doing a PATTERN SETUP action
- CLEAR/UNDO 'TRACK' is now 'TRACK TRIGS', and does not touch TRACK SETUP data. COPY/PASTE/UNDO is unchanged - it still manages both TRACK TRIGS and TRACK SETUP data together. This matches behaviour on the Octatrack.
  - You can still clear a track fully (both TRACK TRIGS and TRACK SETUP together) by using the super CLEAR TRACK (FUNC + hold CLEAR)
- Fixed UNDO MELODY not affecting trig conditions
- Fixed UNDO MACHINE and LOCKS not working

#### OTHER

- Fixed transpose not applying when adjusting during playback
- Fixed transpose being undone on STOP after pattern change had occurred during playback
- Added TRACK LED BLINK toggle in GLOBAL > CONTROL > MECH SETTINGS
- Fixed uneven PAGE LED blinking at 3/4x and 3/2x speeds
- Fixed track LED blink missing trigs around wrap
- Slightly increased duration of track LED blink while below frequency cap
- Track LED blinking now occurs from any source - external MIDI, trig buttons, multi trig, trig pos, etc. This includes muted tracks that are externally triggered (yellow blink)
- Fixed FUNC+LEFT/RIGHT only shifting trigs within the first page
- Fixed song mode not adhering to per-track loop lengths & wrap after value
- Fixed external MIDI input to set notes not working when speed is not 1x
- Fixed SYSEX RECV crashing on receiving ext data backups
- Fixed ext data syx backups being loaded into empty patterns or trigs
- Fixed a lockup caused by CONTROL ALL under heavy use

## 26512 beta

### Changelog

- Fixed playhead lagging behind trigs
- Fixed playhead not adhering to WRAP AFTER = INF
- Fixed LIVE REC mode not respecting track loop length, speed and wrap
- Fixed FUNC+PAGE not opening TRACK SETUP window while in LIVE REC mode
- Added FUNC+CLEAR/COPY/PASTE/UNDO to PATTERN SETUP window
- Added UNDO to actions that affect TRACK SETUP params
- CLEAR PATTERN now clears TRACK SETUP and PATTERN SETUP params
- Fixed new SysEx command IDs colliding with stock status commands. It was necessary to move some of the new SysEx commands:

```text
Updated commands:

Track select:           F0 00 20 3C 03 00 66 <idx> F7


Updated ext data commands:

Dump current global:    F0 00 20 3C 03 00 62 00 F7
Dump global:            F0 00 20 3C 03 00 62 01 <idx> F7
Dump global range:      F0 00 20 3C 03 00 62 02 <idx> <idx> F7
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

```text
Ext data commands:

Dump current pattern:   F0 00 20 3C 03 00 6E 00 F7
Dump pattern:           F0 00 20 3C 03 00 6E 01 <idx> F7
Dump pattern range:     F0 00 20 3C 03 00 6E 02 <idx> <idx> F7
Restore pattern:        F0 00 20 3C 03 00 6F <idx> 01 <bytes> F7

Dump current global:    F0 00 20 3C 03 00 70 00 F7
Dump global:            F0 00 20 3C 03 00 70 01 <idx> F7
Dump global range:      F0 00 20 3C 03 00 70 02 <idx> <idx> F7
Restore global:         F0 00 20 3C 03 00 71 <idx> 01 <data> F7
```

The new firmware can also restore ext data backups via SYSEX RECV as you would other backups, but is not yet included in SYSEX SEND > ALL, PAT+KIT, SONG+P+K, etc.
