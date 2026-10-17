# Desktop Island

A floating desktop pill for Windhawk that puts time, media controls, weather, hardware readings, and selected system activity within reach. Expand it for more detail or keep it compact.

## Features

- Choose a color theme: **Obsidian** (near-black), **Graphite** (dark gray), or **Porcelain** (light). Accent and hex color controls work with every theme, and transparency can be adjusted separately.
- Click to expand, or enable automatic expansion for selected media apps. A separate exclusion list removes unwanted apps from media detection entirely; it starts empty.
- Choose time only, date only, or both in the idle small pill. Weather is a separate choice, and the selected date can also appear during media playback.
- Keep the pill visible, auto-hide it when idle, or hide or move it to another monitor while a full-screen app or game runs.
- Choose the first, second, third, and fourth extra views from dropdowns. The clock or active media view stays first; disabled views are skipped.
- Island notifications are off by default. When enabled, alerts captured by the Island appear from the pill for 4, 8, or 12 seconds, or stay until dismissed. With history enabled, captured alerts are kept across restarts until cleared. The Notifications view shows one entry at a time; click an entry for its full saved text, source, and capture time, or use the right-click menu to copy them. A test alert checks the pop-up and history without waiting for an external alert.
- Optional Calendar tab, disabled by default, with a passive Calendar Plus event preview when available.
- Individually selectable CPU, RAM, GPU, network, and disk-space cards. Disk space defaults off; the disk target remains C:.
- Optional timer, volume, battery, Bluetooth, clipboard, privacy indicators, weather, and game-overlay information. Weather uses day and night icons, a one-decimal current temperature when available, and selectable wind, feels-like, humidity, forecast-low, and forecast-high cards.

GPU, network, and disk measurements are requested when their visible card or game-overlay metric needs them. Animation defaults to 60 FPS; static idle frames are checked at 10 Hz. In separate 20-second samples on Windows 11 build 26100.6899, the Island process averaged 19% of one CPU core during Spotify playback and 11% while playback was paused. It used about 56 MB working set (32 MB private). These are observations, not a performance guarantee across systems or settings.

## Usage and settings

Click the compact pill to expand the overlay. Hover expansion is optional and disabled by default. Choose a palette and target monitor in the mod's settings, and select which modules to show.

- **Small pill content:** choose **Time only**, **Time and date**, or **Date only** under **Time and date in small pill**. Date choices include month and day or weekday and day. When Weather is enabled, **Show weather in small pill** separately adds or removes the temperature and optional condition icon. At least time or date remains visible in the idle pill. The expanded clock remains available with every choice. During media playback, the compact media pill shows album art and can show the selected date; it does not show the time or weather.
- **Visibility:** Expand on hover is controlled in Windhawk settings. Auto-hide can hide the Island after an idle timeout. Its hover-reveal switch applies only to idle auto-hide; instant-hide mode keeps its hover area steady to avoid repeated folding. Full-screen action defaults to Hide and takes effect immediately even when idle auto-hide is set to Never. A separate full-screen hover-reveal switch defaults off. The other full-screen action moves the Island to the largest other monitor when an app or game fills its home monitor; with only one monitor, Move behaves like Hide. The hide/show shortcut can temporarily reveal a hidden Island.
- **Views:** the default order after the first clock/media view is Weather, Hardware Monitor, Calendar, then Notifications. Choose positions with the four **extra view** dropdowns; there is no text list to type. Only enabled views appear, so turn on **Show Calendar view** or **Enable Island notifications** if you want those cards in the loop. Duplicate choices are skipped and any omitted enabled views follow in the default order. In Notifications, Shift+wheel selects an older alert; click it to inspect the saved details, or right-click to copy them, show a test alert, dismiss the current pop-up, open Windows Reliability Monitor, or clear history. These notification menu actions are hidden when Island notifications are off. Reliability Monitor can help investigate a crash near the saved capture time, but an unverified shell popup alone does not prove one occurred. Clicking a compact alert pop-up also opens its details.
- **Media:** **Exclude apps from media detection** removes matching media sessions from both the compact pill and expanded controls. Enter comma-separated app names, executable names, publishers, or media source IDs. Matching ignores case, spaces, punctuation, and `.exe`; publisher and product matching work when Windows exposes the owning program. If a session is hard to identify, play it, right-click the Island, choose **Copy current media source ID**, and add that ID to the list. **Prevent automatic expansion for these apps** only keeps the Island from opening automatically; those apps can still appear in media controls. Automatic expansion is off by default. Browser tabs that share a browser media identity cannot be excluded individually by site or content type.
- **Notifications:** turn on **Enable Island notifications** to let the Island capture and show alerts and include its Notifications view. It is off by default. Turning it off again pauses capture and hides the view and its right-click actions; saved Island history remains available when you turn it back on. Turning off **Keep Island alert history** clears that history. These controls do not change Windows notifications or the Island's separate volume, battery, and other status indicators.
- **Hardware:** select the CPU, RAM, GPU, network, and disk-space cards individually. Disk space is disabled by default and currently reports the C: drive.
- **Display scaling:** Auto DPI scaling uses the primary monitor's Windows display scaling. If the Island is placed on another monitor with a different scale, use Size scale to adjust it.
- **Calendar:** enable the Calendar tab to make it available in the overlay. Windows Calendar Plus can supply its passive event preview; other Island modules work without that mod.
- **Weather:** **Enable Weather and view** controls weather retrieval and the expanded Weather view. **Show weather in small pill** separately hides the compact weather reading while leaving the expanded view available. Choose an optional city and Celsius or Fahrenheit. **Show weather icon in small pill** hides just the condition icon for a narrower, temperature-only reading. Turning off **Enable Weather and view** stops weather requests and removes weather from both views. Each of the five expanded cards can be switched on or off; wind, feels like, and humidity retain their previous defaults, while today's forecast low and high default off. Selected cards appear in one or two rows below the current condition, with Low to the left of High when both are shown. Open-Meteo supplies the decimal current reading, forecast high/low, current condition, and day/night state; if it is unavailable, the Island uses wttr.in's whole-degree reading. Readings normally refresh every 15 minutes when enabled.

The overlay is a separate desktop pill. It does not add a button to the Windows taskbar.

## Data and privacy

Weather in the small pill and expanded view is enabled by default. wttr.in resolves the selected city or, when no city is configured, estimates location from the network request. Open-Meteo then receives the location coordinates for its current and daily forecast readings. Turning off **Enable Weather and view** stops these requests. Both requests use HTTPS, reject downgrade redirects, and limit response size and read duration. Weather data from [Open-Meteo](https://open-meteo.com/) is provided under [CC BY 4.0](https://open-meteo.com/en/terms); the Island changes units, rounds the displayed values to one decimal, and maps condition codes to its own icons. The provider link is also available from the Island's **Weather data credits** right-click action. A one-decimal forecast value is more detailed than wttr.in's whole-degree value, but it may still differ from another weather app or a local thermometer. Clipboard and notification previews can display sensitive content on screen and have their own settings.

Island alert history stores the captured app name, alert text, source, time, and available shell-window metadata in Windhawk local mod storage until you clear it or turn off the history setting. The master notification switch pauses new capture and hides the Island history view without deleting saved entries. History can include sensitive text. Some shell windows expose only a host name such as “Windows Shell Experience Host.” The Island marks these as unverified shell popups with their cause unknown; the process name alone does not establish a crash or restart. Older entries cannot gain details that were never captured. The Island does not independently monitor process or driver crashes, reliably receive every Windows toast, replace Windows Notification Center, or suppress Windows banners. Keep Windows notifications enabled if you want Windows to retain its own notification history; see [Microsoft's notification settings guide](https://support.microsoft.com/en-us/windows/experience/notifications-and-do-not-disturb-in-windows). Do Not Disturb suppression can prevent alerts from entering Island history.

The optional Calendar tab reads a local, unencrypted snapshot from Windows Calendar Plus containing event titles, start/end times, and all-day status. It checks at most once a minute and rejects snapshots older than two hours. Calendar Plus is not required for the overlay; the bridge adds no event editing or reminder notifications.

## Compatibility and status

Experimental source release. Compilation, compact and expanded clock views, date options, auto-hide and full-screen actions, view order, media exclusions, alert history, and weather layout were checked on one multi-display Windows 11 installation. Browser and game-client media sessions were excluded in live checks; matching an additional browser passed source-level checks but has not been tested live. Alert details, persistence, dismissal, and clearing passed live checks. Weather card switches, one-decimal readings, day/night icons, and the compact weather-icon toggle passed live checks; the whole-degree fallback has not been checked live. A test Windows toast appeared in Windows but was not captured by the Island, so Windows-wide notification replacement is not claimed. Compatibility across other Windows builds remains unverified. The overlay runs in a separate Windhawk tool process and does not add a taskbar button. File Tray and its drop handlers have been removed.

Version 0.1.8 places Low before High in the settings and Weather card row. It also orders the controls by placement, animation, theme, privacy, clock, media, alerts, calendar, weather, hardware, game overlay, and system status. All 97 setting paths and defaults remain the same, preserving saved choices. The source compiled, and a live check confirmed the grouped controls, retained selections, and Low/High card order.

Version 0.1.9 added **Enable Island notifications**, initially on by default; version 0.1.13 changes its default to off. Switching it off pauses Windows toast polling and shell alert capture, closes any visible Island alert, and removes Notifications from the view order and its actions from the right-click menu. Saved history is retained until cleared or the separate history setting is turned off. A live Windhawk check of the earlier version confirmed that the view and test-alert action disappear when disabled, then saved history and test alerts work again when enabled.

Version 0.1.10 adds **Time only**, **Date only**, and **Time and date** choices for the idle pill. It always displays at least time or date. A separate switch hides compact weather while keeping the Weather view when weather is enabled. The existing weather master switch still disables all weather and its network requests. Existing saved date choices retain their previous behavior. The source compiled, and a live Windhawk check confirmed all three time/date choices, both compact weather switch states, and access to the expanded Weather view while compact weather was hidden.

Version 0.1.11 removes the unreliable real Windows blur and acrylic backdrop modes, along with their dedicated fill-opacity and acrylic-tint settings. The Island continues to offer pill transparency, background tint intensity, depth shading, and a soft shadow. Saved choices for those remaining settings are unchanged; previously saved backdrop values are ignored. A live Windhawk check confirmed the backdrop controls are gone and pill transparency and soft shadow still work.

Version 0.1.12 removes the redundant **Custom Colors** theme choice from settings and the right-click menu. Accent color mode, custom accent hex, and individual background, text, and border hex overrides remain available with Obsidian, Graphite, and Porcelain. Previously saved Custom Colors selections fall back to Obsidian while nondefault hex overrides remain active. A live Windhawk check confirmed that the choice is gone and accent controls still work with Obsidian and Graphite. The settings audit also clarified Auto DPI scaling's primary-monitor behavior and removed unused internal setting copies without changing the controls.

Version 0.1.13 changed the default scrollable view order to Weather, Hardware Monitor, Calendar, then Notifications. Island notifications now default off, and their right-click actions are hidden while off. Existing saved notification choices remain selected after an update; turn **Enable Island notifications** off in Windhawk if you want the new default on an existing installation.

Version 0.1.14 replaces the comma-separated View order text field with four dropdowns. This makes the order explicit and avoids a text edit that appears ineffective when the named views are disabled. The old text field is no longer used; choose positions once with the new controls if you had customized it. Changing a dropdown resets the expanded view to the first clock/media card before scrolling in the new order.

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
