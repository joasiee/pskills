# Work item comment

The readers follow the item: the assignee, the tester, the product owner, and often the colleague who reported it. Write so the least technical of them can follow, usually the product owner.

- The first sentence is the news: a state, a finding, or a question.
- Status: what is done, with links, what is next, and who owns the next step. "Fixed on 2.3 and 2.4 (PR !101, !102). 2.5 waits for review."
- Finding: what you found, the evidence (a log line, numbers, a link), and what it changes for the fix.
- Question: @mention the person who must answer. One question per comment, with the options if you have them. Give them enough to decide: what changes for customers either way, and what each option costs.
- Explain file names, record types and abbreviations the product owner may not know, or describe them instead: "discount records", not "`DR` records".
- Hand-over to test: what to test, on which environment and version, and the expected result.
- A scope change after someone picked up the item goes in a comment. Edit the description only to correct it.
- One to five sentences. Link the PR instead of repeating its description.
