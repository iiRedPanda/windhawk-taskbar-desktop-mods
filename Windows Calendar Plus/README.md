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

Version 0.2.3 keeps the Google accounts menu focused on connected accounts and sign-in. Sign-in is inactive until the Google OAuth client details are saved in Windhawk. Hover over the dimmed item for setup guidance, and follow the steps below. The source compiles, and the calendar and account-request checks pass. A live check without OAuth settings confirmed the dimmed sign-in item, its hover tip, the simplified menu, and that clicking it does not open a browser.

## Connect a Google account

**Sign in with Google** stays dimmed until you complete this one-time setup. The mod does not ship a shared Google OAuth client, so each user needs a Google Cloud **Desktop app** client. After that, sign-in opens in your default browser.

1. Open the [Google Cloud Console](https://console.cloud.google.com/). Create a project or select one you already have, then [enable the Google Calendar API](https://console.cloud.google.com/apis/library/calendar-json.googleapis.com) in it.
2. Open **Google Auth platform → Branding** and complete the consent setup with an app name and your email. Choose **External** under **Audience** for a personal Google account and add the account you will use under **Test users** while the app is in Testing. Under **Data Access**, add the Calendar scopes ending in `calendar.events.readonly` and `calendar.calendarlist.readonly`.
3. Under **Google Auth platform → Clients**, create a client of type **Desktop app**. Copy its **Client ID** and **Client secret**. You do not need to run Google's sample code or enter a redirect URL.
4. In Windhawk, open **Windows Calendar Plus → Settings**, paste those two values into **Google OAuth client ID** and **Google OAuth client secret**, and save.
5. Open the Windows calendar pane and select **⋯ → Google accounts → Sign in with Google**. Choose your account in the browser and allow read-only calendar access. Reopen **Google accounts** to see the connected account; use **Refresh events** if events have not appeared yet.

Google's [Calendar API quickstart](https://developers.google.com/workspace/calendar/api/quickstart/python) shows the current Cloud Console screens; only its Cloud setup sections apply here. If Google blocks sign-in during Testing, check that the exact email is listed under **Audience → Test users**. Testing-mode Google Calendar access expires after seven days; see [Google's publishing-status guidance](https://support.google.com/cloud/answer/15549945?hl=en) before switching to **In production**, which can show an unverified-app warning or require verification.

One Desktop app client can connect up to four Google accounts. Calendar IDs are optional; otherwise selected calendars are used. Existing Tray Agenda sign-ins are separate and are not copied. Do not publish your client details or a Windhawk settings export containing them.

**Simpler view-only option:** If you only need events from one Google calendar, [copy its secret iCal address](https://support.google.com/calendar/answer/37648?hl=en) and paste it under **ICS feed URLs** instead. This does not connect a Google account or require OAuth setup. Use `Label|https://...` to name a feed. Outlook HTTPS feeds and webcal links also work. Local ICS files are not supported by this provider. Never post private feed URLs publicly.

## Timezones

Timed events are resolved by date-aware IANA/Windows timezone rules, then displayed in the Windows timezone. Recurring instances are expanded before display, so each date has its own daylight saving conversion. All-day end dates remain exclusive. Manual correction defaults to zero and applies only to timed events in the native pane; use it only for a broken feed. Unknown named timezones and unsupported recurrence rules are skipped with a partial-data warning rather than guessed. Custom VTIMEZONE definitions are not interpreted; their TZID must match a known IANA or Windows zone. The ICS expander supports DAILY, WEEKLY, MONTHLY and basic YEARLY rules, COUNT/UNTIL, BYDAY/BYMONTHDAY/BYMONTH, WKST, EXDATE/RDATE and individual overrides. BYSETPOS and other advanced rules are unsupported.

## Range and refresh

Default range is 30 days back and 90 days ahead, configurable up to 90/180. Provider limits: 16 calendars, 2000 events per calendar, 4000 events total, 512 occurrences per ICS event. Dates outside the downloaded range can be empty. The native calendar reads updates every 1.5 seconds while its process is running. The three-dot menu offers Refresh events (normally within 15 seconds, plus network time) and Go to today. Account requests are also handled by the provider in Explorer, normally within 15 seconds. Reopen Google accounts to see the latest account list. Partial/stale calendar states are shown. Shared snapshots are limited to 32 million UTF-16 code units; a larger or unreadable snapshot retains previously readable data and shows an error.

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
