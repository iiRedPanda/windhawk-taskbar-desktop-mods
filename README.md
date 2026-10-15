# Windhawk Taskbar and Desktop Mods

Five independent Windhawk mods for the Windows 11 taskbar, desktop, and calendar. They are modified forks of existing Windhawk projects. Each mod has its own source, settings, README, and license; install or enable only the ones you want.

| Mod | What it does |
| --- | --- |
| [Taskbar Appearance](Taskbar%20Appearance/README.md) | Frosty Matter, WinXP, Windows 7, Translucent, and Command Center themes; Start button styling; optional time and date formatting. |
| [Taskbar Auto-Hide](Taskbar%20Auto-Hide/README.md) | Independent auto-hide policy and animation speed controls. |
| [Taskbar Tray](Taskbar%20Tray/README.md) | System icon, notification bell, battery color, and Show Desktop controls. |
| [Desktop Island](Desktop%20Island/README.md) | A separate desktop pill with media controls, clock and date, optional calendar, selected hardware metrics, and captured-alert history. |
| [Windows Calendar Plus](Windows%20Calendar%20Plus/README.md) | Native calendar agenda with Google and ICS support, reminders, and an optional passive preview for Desktop Island. |

The mods can run independently. Windows Calendar Plus supplies an optional event preview to Desktop Island; neither requires the other for its main functions. Taskbar Appearance formats time and date, while Desktop Island handles optional live information.

## Status and compatibility

All five sources compile with Windhawk 1.7.3. Core taskbar and Island behaviors were checked on one Windows 11 Pro 24H2 system (build 26100.6899) with multiple displays. Calendar parsing, recurrence, cache, account-request, and Island bridge checks pass. Each mod README lists the live checks and remaining limits. Compatibility with other Windows builds, ExplorerPatcher, and StartAllBack has not been established as a general guarantee.

This repository is an experimental source release. The five mods have been submitted as separate pull requests to the official Windhawk mod catalog and are awaiting maintainer review. Submission does not mean catalog acceptance. Report a reproducible issue with the mod version, Windows build, Windhawk version, enabled taskbar customizers, and relevant settings.

## Windhawk catalog submissions

| Mod | Pull request |
| --- | --- |
| Taskbar Appearance | [#6261](https://github.com/ramensoftware/windhawk-mods/pull/6261) |
| Taskbar Auto-Hide | [#6260](https://github.com/ramensoftware/windhawk-mods/pull/6260) |
| Taskbar Tray | [#6259](https://github.com/ramensoftware/windhawk-mods/pull/6259) |
| Desktop Island | [#6262](https://github.com/ramensoftware/windhawk-mods/pull/6262) |
| Windows Calendar Plus | [#6263](https://github.com/ramensoftware/windhawk-mods/pull/6263) |

Each submission is a modified fork. The source files and individual READMEs credit the original authors and retain the applicable license notices.

In separate 20-second samples, the revised Desktop Island process averaged 19% of one CPU core during Spotify playback and 11% while playback was paused, with roughly 56 MB working set. Other hardware and settings have not been measured, so the collection makes no general performance claim.

## Source and licensing

Each folder contains one `.wh.cpp` Windhawk source file with embedded settings and README, plus a matching standalone README and license. The taskbar and calendar forks use GPLv3; Desktop Island uses MIT. Upstream authors and source links are credited in the individual READMEs. Remote theme artwork is referenced but not bundled.

The collection contains source and public documentation only. Personal settings exports, credentials, build outputs, and compiled DLLs are not included.
