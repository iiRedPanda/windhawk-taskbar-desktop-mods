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

## Choose how to add Google Calendar

### Recommended for simple viewing: a private iCal link

Choose this when you want to show events from one or a small set of personal calendars. It is the easiest option: no Google Cloud project, browser sign-in, client secret, or seven-day OAuth expiry.

**Advantages:** quick to set up, read-only, and you can add more than one calendar feed. **Tradeoffs:** it does not create a connected Google account in the calendar menu, each calendar needs its own private link, and anyone who has a link can read that calendar. Treat the link like a password.

1. In the Google Calendar website, open **Settings**, select the calendar in the left sidebar, then open **Integrate calendar**.
2. Copy its **Secret address in iCal format**. Google documents this path in its [private calendar address guide](https://support.google.com/calendar/answer/37648?hl=en).
3. In **Windows Calendar Plus → Settings**, paste the address into **ICS feed URLs**. Use `Label|https://...` to give a feed a name, then save and choose **Refresh events** from the calendar menu.

Keep private feed links out of screenshots, posts, and settings exports. Outlook HTTPS feeds and `webcal` links also work; local ICS files do not.

### Google account sign-in: more setup, better account integration

Choose this when you want the Google accounts menu, up to four connected accounts, and calendars selected through your Google account. Access is read-only. This route needs a Google Cloud **Desktop app** client because the mod deliberately does not ship a shared client.

**Sign in with Google** stays dimmed until its client details are saved in Windhawk. When setup is complete, it opens your default browser for Google sign-in.

#### One-time setup

Select the same project in the Google Cloud Console's top bar before following each link below. Google's current menu is **Google Auth platform**; older guides may call it **APIs & Services → OAuth consent screen**. Already have a working Desktop app client? Start at step 5.

1. Open the [Google Cloud Console](https://console.cloud.google.com/). Create or select a project, then [enable the Google Calendar API](https://console.cloud.google.com/apis/library/calendar-json.googleapis.com) in that project.
2. Open [**Google Auth platform → Branding**](https://console.cloud.google.com/auth/branding). If prompted, choose **Get started**. Enter an app name, support email, and contact email. Choose **External** as the audience for a personal Google account.
3. Open [**Data Access**](https://console.cloud.google.com/auth/scopes) and choose **Add or Remove Scopes**. Under **Manually add scopes**, add `https://www.googleapis.com/auth/calendar.events.readonly` and `https://www.googleapis.com/auth/calendar.calendarlist.readonly`, then choose **Add to Table → Update → Save**.
4. Open [**Clients**](https://console.cloud.google.com/auth/clients), choose **Create client**, and select **Desktop app**. Copy the **Client ID** and **Client secret** when Google shows them. You do not need to run sample code or enter a redirect URL.
5. Open [**Audience**](https://console.cloud.google.com/auth/audience). Under **Publishing status**, choose **Publish app**, then **Confirm** to change **Testing** to **In production**. This removes Google's special seven-day Testing authorization expiry. If it already says **In production**, leave it as is.
6. In Windhawk, open **Windows Calendar Plus → Settings**, paste the ID and secret into **Google OAuth client ID** and **Google OAuth client secret**, then save.
7. Open the Windows calendar pane and select **⋯ → Google accounts → Sign in with Google**. Choose your account in the browser and allow read-only calendar access. Reopen **Google accounts** to see the connected account; use **Refresh events** if events have not appeared yet.

If you previously signed in while the project was still in Testing, sign in again after publishing to get a fresh authorization. Google documents the [seven-day Testing expiry and Publish app action](https://support.google.com/cloud/answer/15549945?hl=en). For personal use by you or a few people you know, Google describes an [exception to verification](https://developers.google.com/identity/protocols/oauth2/production-readiness/sensitive-scope-verification#exceptions-to-verification-requirements), but an unverified app may show a warning and has a user cap. Only continue through that warning if you recognize and trust the OAuth project you created. **In production** removes the special seven-day Testing limit, though Google can still invalidate a token for other reasons. If **Publish app** is missing, confirm that you selected the correct project and check whether Audience already says **In production** or Google lists unfinished setup tasks.

Calendar IDs are optional; otherwise selected calendars are used. Existing Tray Agenda sign-ins are separate and are not copied. Do not publish your client details or a Windhawk settings export containing them.

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
