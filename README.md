# FourTwoRun apps

Mini-apps and utilities by FourTwoRun, namespaced by hardware platform. Each app is its own subdirectory with its own `app.json`; shared brand tokens and helpers live in `shared/`.

## Layout

```
apps/
├── zepp/                      ← Zepp OS (Amazfit, Zepp Health watches)
│   └── fourtworunvoice/       ← Voice notes: talk into the watch, route to an inbox, let an agent process it.
└── shared/                    ← Reused across apps (brand tokens, helpers)
```

When other platforms ship, they get parallel top-level namespaces (`apple/`, `garmin/`).

## Apps

| App | Platform | Status | Description |
|---|---|---|---|
| [`zepp/fourtworunvoice`](zepp/fourtworunvoice) | Zepp OS (Cheetah 2 Pro) | Scaffold | Record a voice note on the watch, route it to an inbox, and have an agent (e.g. Grok Bot) process it. |

## Building an app

From inside any app directory:

```
cd zepp/fourtworunvoice
zeus dev       # local simulator
zeus preview   # QR sideload to a paired watch
zeus build     # produce the .zab bundle
```

Prereqs: zeus CLI installed (`npm i -g @zeppos/zeus-cli`), Developer Mode on, watch connected via Bridge. Full procedure in the private wiki: `~/repos/fourtworun/runfourtworun/setup/zepp-toolchain.md`.

## Brand

All apps use the FourTwoRun visual system: solid black background, `#22CFCB` foreground only, **Inter Black** font. Detailed rules in the private wiki: `~/repos/fourtworun/runfourtworun/brand/identity.md`.

## License

TBD per app. Most likely MIT once anything publishes.
