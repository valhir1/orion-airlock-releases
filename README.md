# ORION Airlock — releases

Installers and auto-update manifests for the ORION Airlock desktop app.

**Binaries only — no source.** This repository intentionally contains no ORION code.

The app is inert without an operator-issued setup code and Cloudflare Access: downloading an
installer does not grant any access to ORION.

## Download

Get the latest installer from the [**Releases**](https://github.com/valhir1/orion-airlock-releases/releases/latest) page:

- **Windows** — the `.exe` (auto-updates itself after the first install).
- **macOS (Apple silicon)** — the `-arm64.dmg`.

## macOS: "ORION Airlock is damaged and can't be opened"

The macOS build is **unsigned** (no paid Apple Developer account), so when you download it
through a browser, macOS quarantines it and shows *"…is damaged and can't be opened"* — sometimes
only offering **Move to Trash**. The app is fine; this is just Gatekeeper blocking an *unsigned
download*. (On macOS Sequoia and later, the old right‑click → **Open** trick no longer bypasses this.)

Use either fix below — both are safe and need **no** Apple Developer account.

### A) Download with `curl` (easiest — needs no developer tools)

Files fetched with `curl` are **not** quarantined, so the app just opens. Open **Terminal** and paste:

```bash
URL=$(curl -sL https://api.github.com/repos/valhir1/orion-airlock-releases/releases/latest \
  | grep -oE 'https://[^"]+arm64\.dmg' | sort -u | head -1)
curl -L -o ~/Downloads/ORION-Airlock.dmg "$URL"
open ~/Downloads/ORION-Airlock.dmg
```

Then drag **ORION Airlock** into your Applications folder and open it normally.

### B) Already downloaded it in a browser?

Remove the quarantine flag, then open the app:

```bash
xattr -dr com.apple.quarantine "/Applications/ORION Airlock.app"
```

If Terminal says `xattr: command not found` (or offers to install developer tools), skip this and
use method **A** above — it needs no tools.

---

Windows builds auto-update from the Releases here. macOS updates are a manual re-download for now
(the auto-updater requires a signed build).
