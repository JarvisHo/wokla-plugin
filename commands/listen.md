---
description: Keep listening to the Wokla watch and answer what it says
allowed-tools: Bash(wokla:*)
---

Start listening to the paired watch, following the wokla skill.

1. Run `wokla status`. If it is not paired, say so and suggest
   `/wokla-plugin:pair`.
2. If a message is already waiting, answer it now, as the skill says.
3. Start a **Monitor** running `wokla listen` with `timeout_ms: 1800000`,
   described as "Wokla watch: messages waiting". Arm it again whenever it
   expires.
4. Say in one line that you are listening, and that it stops when this
   session ends.
