# wokla-plugin

A Claude Code plugin that makes a Claude session the other end of a Wokla
watch: the person on the wrist talks, Claude reads it, answers, and marks it
read.

## Install

```
/plugin marketplace add JarvisHo/wokla-plugin
/plugin install wokla-plugin@wokla
```

Needs macOS. `curl`, `jq`, `say` and `afconvert` all ship with it.

## Use

- `/wokla-plugin:pair 12345` pairs with the code the watch is showing. The
  code lives for 60 seconds.
- `/wokla-plugin:listen` checks every 10 seconds (`WOKLA_INTERVAL`) and
  answers messages as they arrive, for as long as the session is open.
- Or just ask: "看一下手錶", "reply to the watch".

The `wokla` command is on PATH while the plugin is enabled. Run
`wokla help` for the full list.

## The key

`~/.config/wokla/key` is this end of the pairing: whoever holds it is paired
with that watch. It is made on first use and never leaves that file.

- **Moving to another Mac:** copy the file over with scp or AirDrop, and the
  pairing moves with it. Or pair the new Mac afresh.
- **Two Macs with the same key:** listen on only one of them. Two listeners
  answer every message twice.
- **Keep it secret:** never commit it or paste it anywhere.

## Settings

| variable | default |
| --- | --- |
| `WOKLA_HOME` | `~/.config/wokla` |
| `WOKLA_BASE_URL` | `https://api.wokla.app` |
| `WOKLA_VOICE` | `Meijia` (`say -v '?'` lists the rest) |
| `WOKLA_LANGUAGE` | `zh-TW` |
| `WOKLA_MAX_CHARS` | `300` characters at most per message sent; also the ceiling, since the server refuses longer |
| `WOKLA_INTERVAL` | `10` seconds between polls while listening; anything below 2 is raised to 2 |
