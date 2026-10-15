# Windhawk Taskbar and Desktop Mods

Five independent Windhawk mods for the Windows 11 taskbar, desktop, and calendar. They are modified forks of existing Windhawk projects. Each mod has its own source, settings, README, and license; install or enable only the ones you want.

| Mod | What it does |
| --- | --- |
| [Taskbar Appearance](Taskbar%20Appearance/README.md) | Give the Windows 11 taskbar a new look with five presets or return to the Windows default. Frosty Matter creates a split, frosted taskbar with the time above the date. You can also adjust the Start icon, clock and date formatting, seconds, spacing, and click-through gaps. |
| [Taskbar Auto-Hide](Taskbar%20Auto-Hide/README.md) | Choose when the taskbar gets out of the way: when a window is maximized, when a window overlaps it, or according to Windows' own setting. Limit the behavior to certain displays or exclude apps, and optionally adjust show and hide animation speeds separately. |
| [Taskbar Tray](Taskbar%20Tray/README.md) | Clear unwanted indicators from the system tray without hiding the ones you use. Control supported system icons individually, decide when the notification bell appears, change the battery icon to grayscale, and resize or hide the Show Desktop button. |
| [Desktop Island](Desktop%20Island/README.md) | Add an expandable desktop pill for your clock, date, active media controls, selected hardware readings, and optional calendar view. Choose its look and view order, keep Island alerts in a history until you clear them, and hide or move the pill when an app goes full screen. |
| [Windows Calendar Plus](Windows%20Calendar%20Plus/README.md) | See Google Calendar and ICS feed events inside the native Windows calendar pane. Manage accounts and feeds, refresh events, view supported recurring events in the correct local time, and enable reminders. It can also supply an optional event preview to Desktop Island. |

The mods can run independently. Windows Calendar Plus supplies an optional event preview to Desktop Island; neither requires the other for its main functions. Taskbar Appearance formats time and date, while Desktop Island handles optional live information.

## Status and compatibility

All five sources compile with Windhawk 1.7.3. Core taskbar and Island behaviors were checked on one Windows 11 Pro 24H2 system (build 26100.6899) with multiple displays. Calendar parsing, recurrence, cache, account-request, and Island bridge checks pass. Each mod README lists the live checks and remaining limits. Compatibility with other Windows builds, ExplorerPatcher, and StartAllBack has not been established as a general guarantee.

This repository is an experimental source release on GitHub. The mods are not listed in the official Windhawk catalog. Report a reproducible issue with the mod version, Windows build, Windhawk version, enabled taskbar customizers, and relevant settings.

Each mod is a modified fork. Its README credits the original projects and authors and retains the applicable license notices.

In separate 20-second samples, the revised Desktop Island process averaged 19% of one CPU core during Spotify playback and 11% while playback was paused, with roughly 56 MB working set. Other hardware and settings have not been measured, so the collection makes no general performance claim.

## Source and licensing

Each folder contains one `.wh.cpp` Windhawk source file with embedded settings and README, plus a matching standalone README and license. The taskbar and calendar forks use GPLv3; Desktop Island uses MIT. Upstream authors and source links are credited in the individual READMEs. Remote theme artwork is referenced but not bundled.

The collection contains source and public documentation only. Personal settings exports, credentials, build outputs, and compiled DLLs are not included.
