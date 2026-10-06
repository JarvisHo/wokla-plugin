---
description: Unpair this session from the Wokla watch
allowed-tools: Bash(wokla:*)
---

End the pairing with the watch. It cannot be undone from here: the watch is
told "Unpaired", both ends lose the pairing, and the waiting messages go with
it. Pairing again needs a fresh code from the watch.

1. Run `wokla status`. If it is not paired, say so and stop.
2. Ask the user to confirm in one line, naming what happens: the watch is
   told, and pairing again needs a new code. Go on only on a clear yes.
   If they are talking from the watch, ask there with `wokla send`, not in
   the terminal.
3. If a Monitor is running `wokla listen`, stop it first, so it does not
   report `UNPAIRED` as news a moment later.
4. Run `wokla unpair`, then `wokla status` to show `paired: false`.
5. The key in `~/.config/wokla/key` stays. It is this Mac's identity, not
   the pairing, and `/wokla-plugin:pair` uses it again.
