# Desktop Island

A standalone Windhawk desktop overlay for media controls, clock/date, optional calendar, hardware cards, and system indicators.

## Features

- Obsidian, Graphite, Porcelain, and Custom palettes.
- Click-to-expand by default, with optional automatic expansion restricted to an app allowlist and blocklist. Media source filtering ignores Riot Client by default so its launcher session does not displace active playback; the excluded-app list is editable. App matching does not classify browser content as music or video.
- Optional date in the compact pill, including during media playback.
- Clock and date controls appear first in the Modules settings group. The right-click menu no longer overrides the Expand on hover setting.
- Reorder the scrollable views with the View order setting. The clock or active media view stays first; disabled views are skipped.
- Alerts captured by the Island expand from the pill for 4, 8, or 12 seconds, or stay until dismissed. The optional history tab keeps captured alerts across Island restarts until cleared. A right-click test alert checks the pop-up and history without waiting for an external alert.
- Optional Calendar tab, disabled by default, with a passive Calendar Plus event preview when available.
- Individually selectable CPU, RAM, GPU, network, and disk-space cards. Disk space defaults off; the disk target remains C:.
- Inherited timer, volume, battery, Bluetooth, clipboard, privacy indicators, weather, and game-overlay options.

GPU, network, and disk measurements are requested when their visible card or game-overlay metric needs them. Animation defaults to 60 FPS; static idle frames are checked at 10 Hz. In separate 20-second samples on Windows 11 build 26100.6899, the Island process averaged 19% of one CPU core during Spotify playback and 11% while playback was paused. It used about 56 MB working set (32 MB private). These are observations, not a performance guarantee across systems or settings.

## Usage and settings

Click the compact pill to expand the overlay. Hover expansion is optional and disabled by default. Choose a palette and target monitor in the mod's settings, and select which modules to show.

- **Compact date:** choose no date, a short date, or a date with the weekday. The date can also appear during media playback.
- **Visibility:** Expand on hover is controlled in Windhawk settings. Auto-hide can hide the Island after an idle timeout. Its hover-reveal switch applies only to idle auto-hide; instant-hide mode keeps its hover area steady to avoid repeated folding. Full-screen action defaults to Hide and takes effect immediately even when idle auto-hide is set to Never. A separate full-screen hover-reveal switch defaults off. The other full-screen action moves the Island to the largest other monitor when an app or game fills its home monitor; with only one monitor, Move behaves like Hide. The hide/show shortcut can temporarily reveal a hidden Island.
- **Views:** enter `notifications,calendar,weather,hardware` in any order. The first clock/media view stays in place. Shift+wheel on Island alert history pages through older entries; use the right-click menu to show a test alert, dismiss the current alert, or clear the history.
- **Media:** automatic expansion is disabled by default. When enabled, use the app allowlist and blocklist to control which applications trigger it. The separate **Ignore media sessions from these apps** setting excludes nonmedia applications from the media card altogether and defaults to `riot`; edit it if an application is incorrectly included or excluded. A browser playing a show and the same browser playing music share an app identity.
- **Hardware:** select the CPU, RAM, GPU, network, and disk-space cards individually. Disk space is disabled by default and currently reports the C: drive.
- **Calendar:** enable the Calendar tab to make it available in the overlay. Windows Calendar Plus can supply its passive event preview; other Island modules work without that mod.

The overlay is a separate desktop pill. It does not add a button to the Windows taskbar.

## Data and privacy

Weather is enabled by default and uses wttr.in. With no city configured, the service determines location from the network request. Weather requests use HTTPS only, reject downgrade redirects, and limit response size and read duration. Clipboard and notification previews can display sensitive content on screen and have their own settings.

Island alert history stores the captured app name and alert text in Windhawk local mod storage until you clear it or turn off the history setting. It can include sensitive text. The Island does not reliably receive every Windows toast, replace Windows Notification Center, or suppress Windows banners. For native alerts that should remain available without a banner, keep Windows notifications and Notification Center enabled and turn off **Show notification banners** for the relevant app in Windows Settings > System > Notifications; see [Microsoft's notification settings guide](https://support.microsoft.com/en-us/windows/experience/notifications-and-do-not-disturb-in-windows). Do Not Disturb suppression can prevent alerts from entering Island history.

The optional Calendar tab reads a local, unencrypted snapshot from Windows Calendar Plus containing event titles, start/end times, and all-day status. It checks at most once a minute and rejects snapshots older than two hours. Calendar Plus is not required for the overlay; the bridge adds no event editing or reminder notifications.

## Compatibility and status

Experimental source release. Compilation and the compact-to-expanded clock display have been checked on one Windows 11 installation. The date, timed-hide, timed-hover-reveal, instant-hide hover, independent full-screen Hide and hover controls, full-screen Move and return, and view order were checked live. The test alert appeared in the pill and history; Until dismissed, dismissal, persistence after disabling and re-enabling the mod, and clearing history passed live checks. A Windows PowerShell toast appeared in Windows but was not captured by the Island on the tested PC, so Windows-wide notification replacement is not claimed. The broader Windows compatibility matrix remains unverified. The overlay runs in a separate Windhawk tool process and is not inserted beside the Start button. File Tray and its drop handlers have been removed.

## Credits and license

Modified MIT-licensed fork of [Dynamic Island for Windows](https://github.com/devcode90/Dynamic-Island-for-Windows) by Himanshu (devcode90) and contributors. Fork modifications are credited in the source metadata. The upstream MIT notice is included below.

```text
MIT License

Copyright (c) 2026 devcode90

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
