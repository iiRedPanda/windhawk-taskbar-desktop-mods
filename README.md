# Windhawk Taskbar and Desktop Mods

Five independent mods for [Windhawk](https://windhawk.net/), a Windows customization app. They change the Windows 11 taskbar, desktop, and calendar. These are modified forks of existing Windhawk projects; install or enable only the ones you want.

| Mod | What it does |
| --- | --- |
| [Taskbar Appearance](Taskbar%20Appearance/README.md) · [Source](Taskbar%20Appearance/taskbar-appearance.wh.cpp) | Give the Windows 11 taskbar a new look with five presets or return to the Windows default. Frosty Matter creates a split, frosted taskbar with the time above the date. You can also adjust the Start icon, clock and date formatting, seconds, spacing, and click-through gaps. |
| [Taskbar Auto-Hide](Taskbar%20Auto-Hide/README.md) · [Source](Taskbar%20Auto-Hide/taskbar-auto-hide-personal.wh.cpp) | Choose when the taskbar gets out of the way: when a window is maximized, when a window overlaps it, or according to Windows' own setting. Limit the behavior to certain displays or exclude apps, and optionally adjust show and hide animation speeds separately. |
| [Taskbar Tray](Taskbar%20Tray/README.md) · [Source](Taskbar%20Tray/taskbar-tray-personal.wh.cpp) | Clear unwanted indicators from the system tray without hiding the ones you use. Control supported system icons individually, decide when the notification bell appears, change the battery icon to grayscale, and resize or hide the Show Desktop button. |
| [Desktop Island](Desktop%20Island/README.md) · [Source](Desktop%20Island/desktop-island-personal.wh.cpp) | Add an expandable desktop pill for your clock, date, active media controls, selected hardware readings, and optional calendar view. Choose its look and view order, keep Island alerts in a history until you clear them, and hide or move the pill when an app goes full screen. |
| [Windows Calendar Plus](Windows%20Calendar%20Plus/README.md) · [Source](Windows%20Calendar%20Plus/calendar-agenda-plus.wh.cpp) | See Google Calendar and ICS feed events inside the native Windows calendar pane. Manage accounts and feeds, refresh events, view supported recurring events in the correct local time, and enable reminders. It can also supply an optional event preview to Desktop Island. |

## Install in Windhawk

These mods run through [Windhawk](https://windhawk.net/). They are available here on GitHub, but are not in Windhawk's built-in mod catalog.

1. Install and open Windhawk from its official website.
2. Open a mod's **Source** link above, or open its `.wh.cpp` file from the mod's folder. Click GitHub's **Copy raw file** button to copy the complete source code.
3. In Windhawk, click **Create a New Mod**. Replace the sample code in the editor with the copied source.
4. Click **Compile Mod**, then **Exit Editing Mode**. Make sure the new mod is enabled, and adjust its settings as needed.

Repeat for each mod you want. If you already use an original mod that changes the same taskbar or calendar controls, disable it before enabling its fork to avoid overlapping changes. Each mod's README explains its settings and credits the original work.

The mods can run independently. Windows Calendar Plus supplies an optional event preview to Desktop Island; neither requires the other for its main functions. Taskbar Appearance formats time and date, while Desktop Island handles optional live information.

## Status and compatibility

All five sources compile with Windhawk 1.7.3. Core taskbar and Island behaviors were checked on one Windows 11 Pro 24H2 system (build 26100.6899) with multiple displays. Calendar parsing, recurrence, cache, account-request, and Island bridge checks pass. Each mod README lists the live checks and remaining limits. Compatibility with other Windows builds, ExplorerPatcher, and StartAllBack has not been established as a general guarantee.

This repository is an experimental source release on GitHub. The mods are not listed in the official Windhawk catalog. Report a reproducible issue with the mod version, Windows build, Windhawk version, enabled taskbar customizers, and relevant settings.

Each mod is a modified fork. Its README credits the original projects and authors and retains the applicable license notices.

In separate 20-second samples, the revised Desktop Island process averaged 19% of one CPU core during Spotify playback and 11% while playback was paused, with roughly 56 MB working set. Other hardware and settings have not been measured, so the collection makes no general performance claim.

## Source and licensing

Each folder contains one `.wh.cpp` Windhawk source file with embedded settings and README, plus a matching standalone README and license. The taskbar and calendar forks use GPLv3; Desktop Island uses MIT. Upstream authors and source links are credited in the individual READMEs. Remote theme artwork is referenced but not bundled.

The collection contains source and public documentation only. Personal settings exports, credentials, build outputs, and compiled DLLs are not included.
