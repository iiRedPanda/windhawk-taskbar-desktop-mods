# Windows Calendar Plus

Display Google Calendar and ICS events in the native Windows calendar pane, with account management, refresh controls, and optional reminders.

## Features

- Read-only Google Calendar access with up to four accounts.
- HTTPS and webcal ICS feeds, with optional feed labels.
- Date-aware timezone conversion and supported recurring events.
- Configurable event range, reminders, and refresh controls.
- Optional companion integration with Desktop Island for a passive event preview.

## Usage

Configure a Google account or ICS feed as described below, then open the Windows calendar pane to view events. The three-dot menu provides **Google accounts**, **Refresh events**, and **Go to today**. Reminder preferences and the downloaded date range are configured in the mod's settings.

## Compatibility and status

Experimental Windhawk fork. Compilation and calendar parser/cache regression tests have passed; a full live Windows compatibility matrix has not been established. The original Agenda in Calendar View and Tray Agenda can produce duplicate controls or reminders when enabled concurrently with this fork.

## Google Calendar

Use a Google Cloud Desktop-app OAuth client with Calendar API enabled. Paste its client ID and secret into settings, then open the Windows calendar pane and select the three-dot menu > Google accounts > Sign in with Google. Authentication uses the system browser. Use the same menu to see connected accounts and sign out. Calendar access is read-only; up to four accounts are supported. Calendar IDs are optional; otherwise selected calendars are used. Existing Tray Agenda sign-ins are separate and are not copied.

Alternatively paste a Google Calendar secret iCal address under ICS feed URLs. Use Label|https://... to name a feed. Outlook HTTPS feeds and webcal links also work. Local ICS files are not supported by this provider. Never post private feed URLs publicly.

## Timezones

Timed events are resolved by date-aware IANA/Windows timezone rules, then displayed in the Windows timezone. Recurring instances are expanded before display, so each date has its own daylight saving conversion. All-day end dates remain exclusive. Manual correction defaults to zero and applies only to timed events in the native pane; use it only for a broken feed. Unknown named timezones and unsupported recurrence rules are skipped with a partial-data warning rather than guessed. Custom VTIMEZONE definitions are not interpreted; their TZID must match a known IANA or Windows zone. The ICS expander supports DAILY, WEEKLY, MONTHLY and basic YEARLY rules, COUNT/UNTIL, BYDAY/BYMONTHDAY/BYMONTH, WKST, EXDATE/RDATE and individual overrides. BYSETPOS and other advanced rules are unsupported.

## Range and refresh

Default range is 30 days back and 90 days ahead, configurable up to 90/180. Provider limits: 16 calendars, 2000 events per calendar, 4000 events total, 512 occurrences per ICS event. Dates outside the downloaded range can be empty. The native calendar reads updates every 1.5 seconds while its process is running. The three-dot menu offers Refresh events (normally within 15 seconds, plus network time) and Go to today. Account requests are also handled by the provider in Explorer, normally within 15 seconds. Reopen Google accounts to see the latest account list and sign-in status. Partial/stale states are shown. Shared snapshots are limited to 32 million UTF-16 code units; a larger or unreadable snapshot retains previously readable data and shows an error.

## Privacy

Google sign-in runs in Explorer with the system browser, loopback redirect and PKCE. Tokens are DPAPI encrypted; no tokens are sent to the calendar process. The mod caches event titles, descriptions, locations and meeting links in per-Windows-user-named Windhawk storage so ShellHost can read them through Windhawk. This cache is local and is not encrypted. Signing out clears the shared event cache and prevents an in-flight fetch from restoring the removed account's events. Remaining accounts and configured ICS feeds are then fetched again.

## Desktop Island preview
When **Share event preview with Desktop Island** is enabled, the active provider writes a small, unencrypted, per-user snapshot at `%LOCALAPPDATA%\WindhawkPersonal\calendar-island-v1.tsv`. It contains up to six event titles, start/end times and all-day flags, with an 8 KB limit. It contains no credentials, event descriptions or meeting links. Desktop Island reads it only when its Calendar tab is enabled. Sharing is disabled by default. Disabling it removes the snapshot. Clearing the event cache or unloading the active provider removes the preview. The preview adds no separate reminders.

## Reminders

Reminder settings apply to the calendar provider. Disable reminders if another app already supplies them. Google reminders are for accepted timed events; ICS reminders can be toggled separately. This fork uses its own Windows Calendar Plus notification identity.

## Credits and license
Native calendar code: Copyright (C) 2026 lonfro and m417z, GPL-3.0. Calendar provider code adapted from Tray Agenda: Rubens Nascimento (chambber), MIT. The combined fork is distributed under GPL-3.0-only, retaining the original notices.

MIT License (Tray Agenda portions)
Copyright (c) 2026 Rubens Nascimento
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the Software), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED AS IS, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
