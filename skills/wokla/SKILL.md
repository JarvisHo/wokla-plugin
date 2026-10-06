---
name: wokla
description: Talk with the person on the paired Wokla watch. Use when the user asks to check, read or answer the watch ("看一下手錶", "watch messages", "reply to the watch"), when a `wokla listen` monitor reports a MESSAGE line, or when pairing this session with a watch.
---

# Wokla: this session as the other wrist

Wokla is a watch app: one message each way, and the server keeps only the
latest. This session can be the other end of a pairing through the `wokla`
command, which is on PATH while this plugin is enabled.

## Commands

| | |
| --- | --- |
| `wokla status` | Pair status as JSON: `paired`, `inbound`, `outbound` |
| `wokla listen` | Polls every `WOKLA_INTERVAL` seconds (10 by default, 2 at least). Prints one line per message waiting, and nothing otherwise |
| `wokla send "<text>"` | Sends the words. Falls back to speech on a server that does not take words alone yet |
| `wokla say "<text>"` | Speaks the text and sends the recording |
| `wokla seen <created_at>` | Reports a message as read |
| `wokla fetch` | Downloads a waiting message's audio |
| `wokla pair <code>` / `wokla code` / `wokla unpair` | Pairing |

The device key is `~/.config/wokla/key`. It *is* the pairing. Never print
it, paste it, or commit it.

## Reading a message

`inbound` in `wokla status`, or a `MESSAGE` line from `wokla listen`:

- `created_at` names the message. Every report about it uses this number.
- `transcript` / `words=` is what was said.
- `has_words: true` with no transcript yet means the words are still coming.
  Wait for them rather than answering a message you have not read.
- `has_words: false` means no words will come. Nothing here can listen to
  audio: tell the user a voice message arrived that you cannot read, and do
  not mark it seen — the person on the watch would be told it was heard.
- `seen: true` means it has already been taken in. Do not answer it again.

## Answering

1. Read the words.
2. Answer with `wokla send "<reply>"`. Answer the way someone speaks to a
   wrist: one or two short sentences, in the language they used, no
   markdown, no lists. A long answer belongs in this terminal, with a short
   line on the watch saying so.

   `wokla send` refuses anything over `WOKLA_MAX_CHARS` characters (300 by
   default) and sends nothing. When it says "say it shorter", rewrite the
   reply to fit and send again. Do not split it across several messages:
   the watch keeps only the latest, so every one but the last is lost.
3. Then `wokla seen <created_at>`, naming the message you read.
4. Tell the user what was said and what you sent.

## Listening

To keep answering without being asked, run `wokla listen` under the
**Monitor** tool with `timeout_ms: 1800000`, and describe it as
"Wokla watch: messages waiting". Each `MESSAGE` line is one message to
answer as above.

- When the monitor expires, arm it again.
- `UNPAIRED`: the watch left. Stop listening and tell the user.
- `ERROR`: tell the user once. `RECOVERED` follows when it clears.

Only one listener per key. Two sessions or two Macs listening answer
everything twice.

## Pairing

The watch shows a 5-digit code that lives for 60 seconds. Run
`wokla pair <code>` the moment the user gives it to you. Wrong guesses are
rate-limited, so do not try variations of a code that failed — ask for a
fresh one.
