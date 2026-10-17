# Settings audit

This review covers the five mods in this repository. It checks whether each exposed setting is read by its mod, whether its control has a purpose, and whether the wording describes any important condition. Source review cannot prove that every Windows build renders every option correctly; live results are described in each mod's README.

| Mod | Exposed settings | Result |
| --- | ---: | --- |
| Desktop Island | 99 | Every setting has a runtime read. The redundant Custom Colors theme choice was removed; accent and hex overrides remain available with every color theme. Auto DPI scaling is functional, but uses the primary monitor's scale. Its description now says so. The former view-order text entry was replaced with four dropdowns. |
| Taskbar Appearance | 50 | Every setting has a runtime read. The ineffective Frosty Matter split-gap control was removed. Clock controls work independently of the selected taskbar theme. Some clock dimensions and the legacy-taskbar switch only apply to the older taskbar path. |
| Taskbar Auto-Hide | 9 | Every setting has a runtime read. Policy and speed controls are independent. Native Windows 11 speed changes require Windows animation effects; frame rate applies to the legacy taskbar path. |
| Taskbar Tray | 12 | Every setting has a runtime read. Each icon switch applies when Windows exposes that icon. Bell behavior and Show Desktop width use their selected modes and values. |
| Windows Calendar Plus | 26 | Every setting has a runtime read. Google account, ICS feed, reminder, pane, and optional Island preview settings apply to their corresponding enabled features. |

The audit also checked option values against the parsing paths, defaults and schema, and removed unused internal copies of Desktop Island settings. No further setting was confirmed to be a no-op, so conditional controls were kept for users whose Windows build, taskbar, hardware, or chosen module supports them.

The source-reference check is reproducible with `Taskbar tweaks plus/review/audit_setting_references.py` in the development workspace. This report records source review and earlier live checks on one Windows 11 multi-monitor system; it does not claim a live test of every option on every supported configuration.
