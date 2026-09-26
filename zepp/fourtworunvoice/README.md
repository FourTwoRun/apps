# FourTwoRun Voice

Talk into the watch, record a voice note, get it routed to an inbox and processed by an agent (e.g. Grok Bot).

## Status: scaffold only

This is the stock `zeus create` Empty template (APP type, API 4.0, with app-side + settings components), customized only for naming (`app.json`) and target device (`cheetah-2-pro`, round, 466 design width, matching the other FourTwoRun Zepp projects). None of the actual behavior is implemented yet.

## What's here

- `page/index.js` — the watch-side UI (device page). Currently just the template's `console.log`.
- `app-side/index.js` — the companion service that runs in the Zepp phone app. **This is where network calls have to happen** — Zepp OS mini-apps can't make network requests directly from the watch; only the app-side (phone) component can. Currently just the template's `console.log`.
- `setting/index.js` — settings page shown in the Zepp app (e.g. for configuring the inbox destination). Currently just the template stub.
- `assets/default.{r,b,s}/icon.png` — placeholder icons for round/square/band device families.

## What's not built yet

- **Voice capture on the watch.** Need to find the right Zepp OS 4.0 API for microphone recording (check `@zos/*` modules available at this API level) and wire it into `page/index.js`.
- **Getting the recording (or its transcript) from the watch to the phone.** Watch-side and app-side components talk over Zepp's messaging API (`Messaging` / `MessageBuilder` from `@zos/ble` or similar — confirm exact module for API 4.0).
- **The inbox destination.** Where does the app-side component POST the note to? Options to decide: a webhook into something like the [`brainor`](https://github.com/jttraino) inbox pattern, a dedicated endpoint, or directly into whatever queues work for an agent.
- **Agent processing.** How Grok Bot (or another agent) picks up and acts on a routed note — this is unscoped; depends on what "processed by an agent" should actually produce (a brainor-style note, a task, a reply back to the watch, etc.).
- **Settings UI.** Whatever configuration the inbox destination needs (auth token, endpoint URL) should probably live in `setting/index.js` rather than being hardcoded.

## Building

```
cd zepp/fourtworunvoice
zeus dev       # local simulator
zeus preview -t "Amazfit Cheetah 2 Pro"   # QR sideload to a paired watch
zeus build -t "Amazfit Cheetah 2 Pro"     # produce the .zab bundle
```

Prereqs and gotchas: `~/repos/fourtworun/runfourtworun/setup/zepp-toolchain.md` (private wiki).

**Note:** unlike the watch faces in `FourTwoRun/watchfaces`, the `zeus-cli` Empty template for `appType: APP` at API 4.0 works fine out of the box — the "Empty template trap" documented in the private wiki's toolchain notes is specific to `appType: WATCHFACE`, not regular apps.
