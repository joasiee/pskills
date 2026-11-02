# Chat message

A direct message the user pastes into a chat with one colleague. For a post in a team channel, use `announcement.md`.

- Do not draft a chat message that repeats a PR comment. The PR thread is enough.
- A short casual opener is fine: "Hey!", or "Ben er even ingedoken en ..." when you looked into something first. No sign-off.
- A question goes first, and the context comes after, in one or two sentences.
- A request for the colleague to do something (IT, another team) gives the context first, then asks politely whether it is possible: "Zou het mogelijk zijn om ...?". Do not open with the request.
- Ask, do not assert: "Do you know if ...?", "I think ... could ...", "... lijkt ...". The colleague usually knows the code better.
- Casual tone: lowercase product names ("defender", "claude code") are fine.
- An ask says what you need, and by when if that matters.
- One topic per message, one to four sentences.
- Link instead of pasting long text.
- Plain text with backticks for names. No headings.

## Examples

The user's rewrite of a question:

> Hey! Do you know if the runner can send `/status` before `/transcript` for the same turn? If so, i think a run that stopped on a question could ring "task completed" in the bell while the list shows "Awaiting reply".

The user's rewrite of a request to IT:

> Ben er even ingedoken en defender lijkt bij elke achtergrondsessie die ik in claude code start een actie te blokkeren, al start de sessie daarna gewoon. Claude probeert zo'n sessie als een nieuw `claude.exe`-proces via WMI te starten, en dat valt onder de ASR-regel "Block process creations originating from PSExec and WMI commands" (`d1e49aac-8f56-4280-b9ba-993a6d77406c`). In de melding start hij alleen zijn eigen executable. Zou het mogelijk zijn om voor die regel een uitzondering toe te voegen voor `C:\Users\*\.local\bin\claude.exe`?
