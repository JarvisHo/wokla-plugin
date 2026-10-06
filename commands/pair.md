---
description: Pair this session with a Wokla watch using the code it shows
argument-hint: <5-digit code>
allowed-tools: Bash(wokla:*)
---

Pair with the watch. The code lives for 60 seconds, so do this first and
think afterwards.

1. Run `wokla pair $ARGUMENTS`. With no code given, ask the user for the one
   on the watch.
2. If it fails with `invalid_code`, ask for a fresh code. Do not retry
   variations: wrong guesses are rate-limited.
3. Once it is paired, run `wokla status` and say so in one line.
4. Offer to start listening with `/wokla-plugin:listen`.
