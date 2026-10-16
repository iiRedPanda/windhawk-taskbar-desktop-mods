# Taskbar Auto-Hide

Independent controls for taskbar auto-hide policy and animation speed in one Windhawk mod.

## Features

- Windows default, hide for maximized windows, hide for intersecting windows, or never auto-hide.
- Foreground-window filtering, program exclusions, and primary-monitor selection.
- Optional animation override with separate show/hide speed controls.

## Settings

Choose **Auto-hide policy** to follow Windows, hide for maximized or intersecting windows, or keep the taskbar visible. Use **Foreground window only**, **Excluded programs**, and **Primary monitor only** to narrow which windows and displays affect the policy.

**Customize animation speed** changes the duration of supported taskbar animations. If Windows animation effects are disabled, the native taskbar has no visible animation to speed up. This setting does not turn Windows animation effects on.

Enable **Customize animation speed** to change **Show speed percent** and **Hide speed percent** independently. A value of 100 uses the original speed; larger values shorten the animation.

Policy and animation default to Windows behavior. The frame-rate setting applies to the legacy taskbar, not the native Windows 11 animation.

## Compatibility and status

Experimental source release. Compilation and the default no-override configuration have been checked on one Windows 11 PC with three displays. The maximized-window policy was checked with desktop, small-window, and maximized-window states. When the mod enabled Windows auto-hide itself, hover reveal became unreliable on all three monitors; version 0.1.1 waits for Explorer's `TaskbarCreated` message before applying the policy, and hover reveal passed live checks on all three monitors both before and after an Explorer restart. Speed customization did not change the visible result there because Windows animation effects were disabled. Other policy modes, animation behavior with effects enabled, and broader Windows compatibility remain unverified. The inherited ExplorerPatcher path is retained; StartAllBack compatibility is unverified. Concurrent policy/speed mods can apply overlapping hooks.

## Credits and license

Modified GPLv3 fork of m417z's [Taskbar Auto-Hide When Maximized](https://github.com/ramensoftware/windhawk-mods/blob/main/mods/taskbar-auto-hide-when-maximized.wh.cpp) and [Taskbar Auto-Hide Speed](https://github.com/ramensoftware/windhawk-mods/blob/main/mods/taskbar-auto-hide-speed.wh.cpp). Version 0.1.1 incorporates the upstream [TaskbarCreated initialization fix](https://github.com/m417z/my-windhawk-mods/commit/e36cbee240792241df6b29328151a0582588f384). Fork modifications are credited in the source metadata.
