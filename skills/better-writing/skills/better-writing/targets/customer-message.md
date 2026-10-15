# Customer message

Any text a customer reads: an email, a reply to a support ticket, an update during an incident, a postmortem after instability or slow performance.

The reader uses the product to do their job. They do not know programming, builds, pipelines or hosting, and they do not need to. They want to know what happened to their work, whether it is fine now, what to expect, and whether they must do anything.

## Tone

- Friendly, concise and to the point.
- Write as the company: "we" for the company, "you" for the reader. "I" only for the person who signs.
- Calm and confident. The reader should finish the message trusting that we understand the problem and have it under control.
- A message to one person may open with "Hi Sarah," and close with "Kind regards,". A message to all users of a customer ("some of you saw ...") has a short title line instead and no greeting or sign-off.
- One sincere apology when the customer lost time or work is fine, not one in every paragraph.

## Not technical

- Describe what the customer saw in their own words and screens: "reports load slowly or not at all", "the export stopped halfway". Use the product names and domain terms they know, and the exact menu or button names.
- When the cause needs explaining, use everyday words a non-developer follows: a server, its memory, its processing capacity, storage. "The server reads the same data from storage again and again" is fine.
- No code, class, file, database, cloud, container, pipeline, build or deployment terms. Not "memory leak", "pod restart", "cache eviction", "thread pool", "hotfix deployed to PROD". Write "we installed an update", "we changed the server schedule".
- No PR numbers, work item numbers or branch names. A version only as the customer sees it: "version 5".
- Times with the date and the time zone the customer uses: "today at about 14:30 CET", "on 2 March".

## How much to share

- Be honest about the effect on the customer. If reports failed, results were wrong, or data must be refreshed, say so plainly and say what we did about it or what they must do.
- Explain the cause only as far as the reader needs to understand it and trust the fix. Leave out the mechanism behind it and internal numbers.
- Show what we already changed, with dates. An earlier problem that we fixed may be mentioned when it shows progress: "Before this change, ... This no longer happens."
- Be honest about what can still happen and when it is fully solved: "A single very large report can still slow down other users on the same server. Version 5 has the full fix." Give a workaround the reader can use until then.
- Do not mention other customers, and do not blame a supplier, a colleague or the customer. We own the service.
- Do not guess. While the cause is unknown, say what we are doing and when the next update comes, not "we think it might be ...". Use "we expect" only for an outcome we have reason to expect.
- Promise only what is certain. Not "this will never happen again", but what we changed and what we expect from it.

## Shapes

All shapes are plain paragraphs. No section headers and no bullet lists inside the message. Numbered steps are the only exception.

### Answer to a question or support ticket

The answer first, then the steps with exact menu names, numbered when there are more than two. End with the result they should see.

### Update during an incident

What the customer sees now, that we are working on it, what they can do meanwhile if anything, and when the next update comes. Two to four sentences.

### Postmortem after instability or slow performance

A short title line that names what the customer noticed, then a few paragraphs. Each paragraph tells one part of the story, so do not split a part over two short paragraphs:

1. What the customer saw and when, the cause, and why that happens in everyday words.
2. What we changed, with dates and times, and what the reader can expect now, including what can still happen.
3. The full fix and when it comes, plus what the reader can do until then.

End there. No summary or TLDR paragraph.

## Overrides of the baseline

- "Use the codebase's names" does not apply. Use the names the customer sees in the product.
- "Name problems plainly" and "give the problem its weight" become: state the effect on the customer honestly, without internal detail or severity labels.
- "A bit tentative" and "I think" do not apply. Be clear about what we know and what we do next.
- A greeting, a sign-off and one apology are allowed.
- Markdown usually does not render in email, ticket or chat tools. Use plain text.

## Example

A message to all users of a customer, written as plain paragraphs. A first draft had a bold header per section and a bullet list for the changes.

> Slow reports in the web app
>
> Today at about 14:30 CET, some of you saw reports load slowly or not at all for a few minutes. One very large report caused this. It covers several years of detailed sales data and needs more data than a server can keep in memory. The server then reads the same data from storage again and again, and uses all its processing capacity while it does. Reports from other users on that server wait until it finishes, which today took about 4 minutes.
>
> We already made two changes. On 2 March we changed the morning server schedule. Before this change, most users moved at 09:00 CET to a new server that had no data loaded yet, so their first reports were slow. This no longer happens. Tonight at 22:10 CET we installed an update, so servers now clear memory without holding up other users. We expect fewer and shorter slow moments, but a single very large report can still slow down other users on the same server.
>
> Version 5 has the full fix. It shares processing capacity fairly between users, so one large report can no longer hold up everyone else, and it manages memory better. Until then, reports with a shorter period of sales data load less data, so they run faster and hold up other users less.
