# Taskbar Appearance

Change the Windows 11 taskbar's look and tune its Start button and clock from one Windhawk mod. Switch themes without giving up independent control of the date and seconds.

## Features

- Choose a taskbar theme: **Frosty Matter** (split frosted panels), **WinXP** or **Windows 7** (classic-inspired styling), **Translucent** (minimal transparent background), **Command Center** (dark app panels), or **Windows default**.
- Frosty Matter combines the split FrostyGlass layout with an optional Matter-style clock: time above date, Tektur when installed, and Segoe UI fallback.
- Adjustable Frosty Matter split gap, Start icon color/effects/size, and empty-area click-through behavior.
- Independent clock switch, date visibility, seconds, formats, locale, typography, and spacing.

## Settings

Choose a preset under **Taskbar theme**. Frosty Matter is the default. Its split-gap setting adjusts the space between the center taskbar and the tray section.

**Click-through empty taskbar area** defaults to Auto. It lets clicks reach the desktop or window behind transparent gaps in Frosty Matter and Command Center. Choose Never to keep the normal taskbar hit area, or Always to use click-through with another theme.

Use **Start button icon color**, the advanced color effects, and **Start icon size percent** to adjust the Start icon independently of the theme.

Enable **Customize clock and date** to control the clock text. Use **Show seconds** and **Clock → Date style → Hide date** to choose the information displayed. For the Frosty Matter layout, keep the time on the top line and date on the bottom line.

Windows default selects no preset theme. Clock, Start overrides, and advanced custom styles remain independent. Date and seconds preferences are shared across themes. Fonts are not installed automatically.

### Clock patterns

Clock line formats support the tokens below, numbered extra time/date formats, configured time zones, and calendar values such as `%weeknum_iso%`. Weather, media, web-feed, and hardware-metric clock tokens are not included in this fork.

| Pattern | Content |
| --- | --- |
| `%time%` | Time using the configured time format |
| `%date%` | Date using the configured date format |
| `%weekday%` | Day of the week using the configured weekday format |
| `%newline%` | A line break |

## Compatibility and status

Experimental source release. Compilation, Frosty Matter's split layout, the seconds/date toggles, Windows default styling with the custom clock, and the WinXP, Windows 7, and Translucent presets have been checked on one Windows 11 installation. The inherited Command Center preset crashed Explorer there; its smaller replacement loads without crashing, has working empty-area click-through, and its app boxes and running dots were reported to look correct on the main and portrait displays. Restore-on-disable behavior and compatibility across Windows builds remain unverified. Avoid overlapping overrides from the original Styler, Start Button Colorizer, or Clock Customization mods. Legacy clock paths are inherited; this does not establish legacy theme support or StartAllBack compatibility.

## Data and limitations

WinXP and Windows 7 reference remote image assets and use the inherited image cache. A first launch without network access can lack those assets. Theme-usage reporting is removed. The clock does not request weather, web feeds, media data, or hardware metrics.

## Credits and license

Modified GPLv3 fork of m417z's [Windows 11 Taskbar Styler](https://github.com/ramensoftware/windhawk-mods/blob/main/mods/windows-11-taskbar-styler.wh.cpp), [Start Button Colorizer](https://github.com/ramensoftware/windhawk-mods/blob/main/mods/taskbar-start-button-colorizer.wh.cpp), and [Taskbar Clock Customization](https://github.com/ramensoftware/windhawk-mods/blob/main/mods/taskbar-clock-customization.wh.cpp). Fork modifications are credited in the source metadata.

Theme designs are credited through the [taskbar styling guide](https://github.com/ramensoftware/windows-11-taskbar-styling-guide): [FrostyGlass](https://github.com/ramensoftware/windows-11-taskbar-styling-guide/tree/main/Themes/FrostyGlass), [Matter](https://github.com/ramensoftware/windows-11-taskbar-styling-guide/tree/main/Themes/Matter), [WinXP](https://github.com/ramensoftware/windows-11-taskbar-styling-guide/tree/main/Themes/WinXP), [Windows 7](https://github.com/ramensoftware/windows-11-taskbar-styling-guide/tree/main/Themes/Windows7), [TranslucentTaskbar](https://github.com/ramensoftware/windows-11-taskbar-styling-guide/tree/main/Themes/TranslucentTaskbar), and [Command Center](https://github.com/ramensoftware/windows-11-taskbar-styling-guide/tree/main/Themes/Command%20Center). Referenced artwork is not relicensed by this fork.
