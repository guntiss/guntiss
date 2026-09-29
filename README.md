### Hi, I'm Guntis

I work as a DevOps engineer, and in my spare time I build useful stuff for myself.

## ⚡ [Kubi](https://github.com/guntiss/kubi)

[![Marketplace](https://vsmarketplacebadges.dev/version-short/guntiss.kubi.svg?label=marketplace)](https://marketplace.visualstudio.com/items?itemName=guntiss.kubi)
[![Installs](https://vsmarketplacebadges.dev/installs-short/guntiss.kubi.svg?label=installs)](https://marketplace.visualstudio.com/items?itemName=guntiss.kubi)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/guntiss/kubi/blob/main/LICENSE)

**Manage Kubernetes clusters in VS Code at lightning speed.** A must have for every Kubernetes admin. Only dependency is `kubectl` and VS Code itself. 

<a href="https://github.com/guntiss/kubi"><img src="https://raw.githubusercontent.com/guntiss/kubi/HEAD/docs/overview.png" width="100%" alt="Kubi's Overview tab: unhealthy pods and Warning events grouped by reason"></a>

Try it out: `code --install-extension guntiss.kubi`

## Self-hosted

<table>
<tr>
<td width="50%" valign="top">

### [Calorie App](https://github.com/guntiss/calorie-app)

<a href="https://github.com/guntiss/calorie-app"><img src="https://raw.githubusercontent.com/guntiss/calorie-app/HEAD/docs/screenshots/day-grid.png" width="32%" alt="The day's log, with remaining macros pinned to the footer"> <img src="https://raw.githubusercontent.com/guntiss/calorie-app/HEAD/docs/screenshots/log-modal.png" width="32%" alt="Logging a food: the weight, then a search over your library"> <img src="https://raw.githubusercontent.com/guntiss/calorie-app/HEAD/docs/screenshots/food-library.png" width="32%" alt="The food library, each entry with its per-100 g macros"></a>

A calorie tracker built around your own foods instead of a crowd-sourced database. The day's log works like a spreadsheet: change an amount and the remaining macros update as you type. Barcode scanning, a planning mode, and installable as a PWA.

<sub>Nuxt 4 · Postgres · Drizzle · Docker</sub>

</td>
<td width="50%" valign="top">

### [Home Energy Dashboard](https://github.com/guntiss/energy-dashboard)

<a href="https://github.com/guntiss/energy-dashboard"><img src="https://raw.githubusercontent.com/guntiss/energy-dashboard/HEAD/docs/images/overview.png" width="100%" alt="Totals across every billing month, and progress towards paying the installation off"></a>

Electricity billing for a home with solar panels and a battery. Every 15-minute interval is priced against Nord Pool spot prices and your tariff, and the supplier's monthly invoice is rebuilt to the cent. It also shows what the system saved and when it pays for itself.

<sub>FastAPI · Vue · SQLite · Docker</sub>

</td>
</tr>
</table>

## Rooted LG TV

<table>
<tr>
<td width="50%" valign="top">

### [WebOS Galaxy Launcher](https://github.com/guntiss/webos-galaxy-launcher)

<a href="https://github.com/guntiss/webos-galaxy-launcher"><img src="https://raw.githubusercontent.com/guntiss/webos-galaxy-launcher/HEAD/docs/screenshot.jpg" width="100%" alt="WebOS Galaxy Launcher on an LG G4: a spiral galaxy, a clock and a row of apps"></a>

Custom home screen app for rooted LG WebOS TV. Get rid of banner ads, sponsored rows and other useless stuff.

<sub>Vue · webOS · Homebrew Channel</sub>

</td>
<td width="50%" valign="top">

### [Magic Remote buttons](https://github.com/guntiss/lg-g4-remote-config)

Remap LG remote buttons to useful functions and home automation

| Button                       | Now does                                       |
|------------------------------|------------------------------------------------|
| Mic                          | Switches between Galaxy Launcher and LG's home |
| Channel + / −                | OLED brightness up / down                      |
| Guide, held 1 s              | Toggle childlock                               |
| … (more actions)             | Screen off                                     |
| Digits, color keys, app keys | Trigger Home Assistant webhooks                |

<sub>Shell · luna-send · Home Assistant</sub>

</td>
</tr>
</table>

## Immich

<table>
<tr>
<td width="50%" valign="top">

### [immich-webos](https://github.com/guntiss/immich-webos)

A webOS TV client for your self-hosted Immich photo and video server, with a fullscreen wallpaper slideshow that turns the TV into a photo frame. A fork of [aneeshtigga/immich-webos](https://github.com/aneeshtigga/immich-webos) with many improvements.

<sub>TypeScript · webOS · Immich</sub>

</td>
<td width="50%" valign="top">

### [Google Photos → Immich sync](https://github.com/guntiss/gphotos-immich-extension)

A Chrome extension that keeps selected Google Photos shared albums in sync with Immich, in the background, using the Google account you're already signed in to. No server, no OAuth app. Photos Immich already has are detected by checksum and never uploaded twice.

<sub>JavaScript · Chrome extension · Immich</sub>

</td>
</tr>
</table>
