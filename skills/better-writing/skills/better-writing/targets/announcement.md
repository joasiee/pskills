# Announcement

A post in a chat channel about a change people must know about or act on. Announcements usually go to the whole company, so most readers are not developers.

## When to write one

Only when readers must act, or will notice the change in their work. A fix or build change that needs no action from anyone is not an announcement. Say so to the user instead of drafting one.

## Shape

1. Title: a short lowercase line that states the news. "new login page on the demo environment", "5 crash fixes landed in version 2.3 this week".
2. What changed, in one or two sentences, as the reader sees it. Start with the news, no greeting. When something prompted the post, such as a retro point or a question in the channel, open with that in one sentence.
3. What it means for the reader: "This means ...". Name what changes in their work, or what they no longer need to do.
4. What the reader must do, with the exact names they will see: the menu, the setting, the environment.
5. A trade-off or workaround, if one exists, with its cost stated plainly. Then your recommendation in the first person, with the reason.
6. A TLDR of one or two sentences when the body is longer than three paragraphs: the change and the action.

The steps set the order, not the paragraphs. Join them into two or three full paragraphs, usually what changed and what it means, then what to do. A row of one- or two-sentence paragraphs reads like a list.

End on the action. No sign-off.

## Details

- No compiler, library, class or build-tool names in a company-wide post. Describe the effect: "the desktop app starts faster", not the mechanism.
- "We" for what the team did, "you" for the reader, "I" for a recommendation.
- Exact names the reader uses: versions, environments, customers, dates, counts. Internal posts name customers, unlike release notes.
- Several items of the same kind (fixes, customers): one bullet each, led by the customer or component name and a colon, with the other fields in the same order every time.

## Developer-only channels

A post in a developers' channel may name tools, branches and settings. The example below is one.

> **clang-format on 2.4**
>
> We upgraded clang-format to version 21 for `release/2.4`. This means we now maintain two versions: 19 for `release/2.3` and older, 21 for everything newer. clang-format 21 is in the shared tools repo, so pull from there.
>
> Format on save in Visual Studio still uses version 19, so it no longer works for 2.4. You can switch it to 21 in the settings, but then you must switch back for 2.3 branches. That is not ideal. I recommend the git hook instead. It formats every commit with the right version, including code Claude wrote. Set `INSTALL_GIT_HOOKS=ON` to configure it automatically.

One bullet from a list of fixes:

> - Acme: crash while saving a report at the end of a run, twice in 72 hours. A cache rebuild freed memory the report writer still read. PR 1234.
