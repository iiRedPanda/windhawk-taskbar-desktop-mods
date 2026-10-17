# Windows Calendar Plus

Bring Google Calendar and ICS feed events into the native Windows calendar pane. View upcoming events, refresh them from the pane, and choose whether to receive reminders.

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

Version 0.2.2 makes Google sign-in clickable on a fresh installation and opens this guide when OAuth client settings are missing. The source compiles and the calendar and account-request checks pass. The new first-run menu path has not yet been verified live on a PC without saved accounts or client settings.

## Connect a Google account

**Sign in with Google** is available in the calendar pane even when no accounts have been added. Once a Google OAuth client is configured, clicking it opens Google's sign-in and consent page in your default browser. This source release does not include a shared OAuth client, so a first-time user must create a Google Cloud Desktop app client once. If the client is missing, clicking **Sign in with Google** explains this and opens this guide instead of leaving a disabled button.

1. Open the [Google Cloud Console](https://console.cloud.google.com/) and create or select a project for Calendar Plus.
2. [Enable the Google Calendar API](https://console.cloud.google.com/apis/library/calendar-json.googleapis.com) for that project.
3. In **Google Auth platform → Branding**, start the OAuth setup and enter an app name, support email, and contact email. Under **Audience**, choose **External** for a personal Google account. If the project is in **Testing**, add the Google account you will sign in with as a test user.
4. Under **Data Access**, add the read-only scopes `https://www.googleapis.com/auth/calendar.events.readonly` and `https://www.googleapis.com/auth/calendar.calendarlist.readonly` if Google asks you to configure scopes. The mod requests these two scopes during sign-in.
5. Under **Google Auth platform → Clients**, create an OAuth client with application type **Desktop app**. Copy its client ID and client secret from the result or downloaded JSON. You do not need to run Google's sample code or add a redirect URL for this desktop client. [Google's Calendar API quickstart](https://developers.google.com/workspace/calendar/api/quickstart/python) shows the current Cloud Console screens.
6. Open **Windows Calendar Plus → Settings** in Windhawk. Paste the values into **Google OAuth client ID** and **Google OAuth client secret**, then save the settings. Do not put these values in a public issue or settings export.
7. Open the Windows calendar pane. Select **⋯ → Google accounts → Sign in with Google**. Your default browser opens Google's account chooser and consent page. Choose your account and grant the requested read-only calendar permissions. Return to the calendar pane, then reopen **Google accounts** to see the connection status; use **Refresh events** if events have not appeared yet.

Google sign-in supports up to four accounts. Calendar IDs are optional; otherwise selected calendars are used. Existing Tray Agenda sign-ins are separate and are not copied. If Google blocks access while your OAuth project is in Testing, check that the exact Google email is listed under **Audience → Test users**. [Google's OAuth desktop app guide](https://developers.google.com/identity/protocols/oauth2/native-app) explains why the OAuth client is needed and how the browser returns to a desktop app.

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
