# Desktop Island

A standalone Windhawk desktop overlay for media controls, clock/date, optional calendar, hardware cards, and system indicators.

## Features

- Obsidian, Graphite, Porcelain, and Custom palettes.
- Click-to-expand by default, with optional automatic expansion restricted to an app allowlist and blocklist. The separate media-source exclusion list is empty by default. Enter an app or executable name, or a publisher name where the owning program can be identified. `riot games` also covers known Riot game names. App matching does not classify browser content as music or video.
- Optional date in the compact pill, including during media playback.
- Clock and date controls appear first in the Modules settings group. The right-click menu no longer overrides the Expand on hover setting.
- Reorder the scrollable views with the View order setting. The clock or active media view stays first; disabled views are skipped.
- Alerts captured by the Island appear from the pill for 4, 8, or 12 seconds, or stay until dismissed. When history is enabled, captured alerts are kept across restarts until cleared. The Notifications view shows one entry at a time; click an entry for its full saved text, source, and capture time, or use the right-click menu to copy them. A test alert checks the pop-up and history without waiting for an external alert.
- Optional Calendar tab, disabled by default, with a passive Calendar Plus event preview when available.
- Individually selectable CPU, RAM, GPU, network, and disk-space cards. Disk space defaults off; the disk target remains C:.
- Inherited timer, volume, battery, Bluetooth, clipboard, privacy indicators, weather, and game-overlay options. Weather uses separate day and night icons for clear and partly cloudy conditions, distinct precipitation icons, a one-decimal current temperature when available, and selectable wind, feels-like, humidity, forecast-high, and forecast-low cards.

GPU, network, and disk measurements are requested when their visible card or game-overlay metric needs them. Animation defaults to 60 FPS; static idle frames are checked at 10 Hz. In separate 20-second samples on Windows 11 build 26100.6899, the Island process averaged 19% of one CPU core during Spotify playback and 11% while playback was paused. It used about 56 MB working set (32 MB private). These are observations, not a performance guarantee across systems or settings.

## Usage and settings

Click the compact pill to expand the overlay. Hover expansion is optional and disabled by default. Choose a palette and target monitor in the mod's settings, and select which modules to show.

- **Compact date:** choose no date, a short date, or a date with the weekday. The date can also appear during media playback.
- **Visibility:** Expand on hover is controlled in Windhawk settings. Auto-hide can hide the Island after an idle timeout. Its hover-reveal switch applies only to idle auto-hide; instant-hide mode keeps its hover area steady to avoid repeated folding. Full-screen action defaults to Hide and takes effect immediately even when idle auto-hide is set to Never. A separate full-screen hover-reveal switch defaults off. The other full-screen action moves the Island to the largest other monitor when an app or game fills its home monitor; with only one monitor, Move behaves like Hide. The hide/show shortcut can temporarily reveal a hidden Island.
- **Views:** enter `notifications,calendar,weather,hardware` in any order. The first clock/media view stays in place. In Notifications, Shift+wheel selects an older alert; click it to inspect the saved details, or right-click to copy them, show a test alert, dismiss the current pop-up, open Windows Reliability Monitor, or clear history. Reliability Monitor can help investigate a crash near the saved capture time, but an unverified shell popup alone does not prove one occurred. Clicking a compact alert pop-up also opens its details.
- **Media:** the media controls are together near the top of Modules. **Exclude apps from media detection** removes matching sessions from the compact pill and expanded media controls; it is empty by default. Entries are comma-separated and match app IDs, executable names, product names, or executable company names when Windows exposes the owning program. `firefox` or `firefox.exe` excludes Firefox; `riot games` excludes recognized Riot Client, VALORANT, League, Teamfight Tactics, Runeterra, and 2XKO sessions. Matching ignores case, spaces, punctuation, and `.exe`. For an app with an unrelated ID, play its media, right-click the Island, choose **Copy current media source ID**, and paste that ID into the exclusion setting. **Prevent automatic expansion for these apps** only stops the Island opening automatically; the app can still appear as media. Automatic expansion is disabled by default. A browser playing a show and the same browser playing music may share a source identity.
- **Hardware:** select the CPU, RAM, GPU, network, and disk-space cards individually. Disk space is disabled by default and currently reports the C: drive.
- **Calendar:** enable the Calendar tab to make it available in the overlay. Windows Calendar Plus can supply its passive event preview; other Island modules work without that mod.
- **Weather:** choose an optional city and Celsius or Fahrenheit. Each of the five expanded cards can be switched on or off; wind, feels like, and humidity retain their previous defaults, while today's forecast high and low default off. The compact pill always shows the current temperature when Weather is enabled. Open-Meteo supplies the decimal current reading, forecast high/low, current condition, and day/night state; if it is unavailable, the Island uses wttr.in's whole-degree reading. Readings normally refresh every 15 minutes.

The overlay is a separate desktop pill. It does not add a button to the Windows taskbar.

## Data and privacy

Weather is enabled by default. wttr.in resolves the selected city or, when no city is configured, estimates location from the network request. Open-Meteo then receives the location coordinates for its current and daily forecast readings. Both requests use HTTPS, reject downgrade redirects, and limit response size and read duration. The Weather view labels the active source. Weather data from [Open-Meteo](https://open-meteo.com/) is provided under [CC BY 4.0](https://open-meteo.com/en/terms); the Island changes units, rounds the displayed values to one decimal, and maps condition codes to its own icons. A one-decimal forecast value is more detailed than wttr.in's whole-degree value, but it may still differ from another weather app or a local thermometer. Clipboard and notification previews can display sensitive content on screen and have their own settings.

Island alert history stores the captured app name, alert text, source, time, and available shell-window metadata in Windhawk local mod storage until you clear it or turn off the history setting. It can include sensitive text. Some shell windows expose only a host name such as “Windows Shell Experience Host.” The Island marks these as unverified shell popups with their cause unknown; the process name alone does not establish a crash or restart. Older entries cannot gain details that were never captured. The Island does not independently monitor process or driver crashes, reliably receive every Windows toast, replace Windows Notification Center, or suppress Windows banners. Keep Windows notifications enabled if you want Windows to retain its own notification history; see [Microsoft's notification settings guide](https://support.microsoft.com/en-us/windows/experience/notifications-and-do-not-disturb-in-windows). Do Not Disturb suppression can prevent alerts from entering Island history.

The optional Calendar tab reads a local, unencrypted snapshot from Windows Calendar Plus containing event titles, start/end times, and all-day status. It checks at most once a minute and rejects snapshots older than two hours. Calendar Plus is not required for the overlay; the bridge adds no event editing or reminder notifications.

## Compatibility and status

Experimental source release. Compilation and the compact-to-expanded clock display have been checked on one Windows 11 installation. The date, timed-hide, timed-hover-reveal, instant-hide hover, independent full-screen Hide and hover controls, full-screen Move and return, and view order were checked live. With Spotify playing, `brave.exe, riot games` in Exclude apps from media detection kept Brave video and Riot Client out of the Island in a live check. Firefox matching passed source-level checks but has not been tested live. The test alert appeared in the pill and history; Until dismissed, dismissal, persistence after disabling and re-enabling the mod, and clearing history passed live checks. Version 0.1.3 adds source and time details and click-to-inspect for history entries, plus location-aware day/night weather icons and more specific precipitation icons; the saved-entry and new-test-alert details windows passed live interaction checks. The weather icon also appeared correctly in a live check. Version 0.1.4 adds per-card weather switches, forecast high/low, and one-decimal Open-Meteo readings with whole-degree fallback; its one-decimal reading and metric switches passed a live check. The revised card-label layout passed live checks with both four and five cards selected. The provider source label and whole-degree fallback have not been checked live. A Windows PowerShell toast appeared in Windows but was not captured by the Island on the tested PC, so Windows-wide notification replacement is not claimed. The broader Windows compatibility matrix remains unverified. The overlay runs in a separate Windhawk tool process and is not inserted beside the Start button. File Tray and its drop handlers have been removed.

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
