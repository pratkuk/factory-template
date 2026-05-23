# learnings/

For tools that iterate against ground truth (filter changes in a screener, threshold tuning in a notifier, prompt revisions in an LLM-backed tool), each iteration's rationale lives here as a dated file BEFORE the change lands in code.

Format: `YYYY-MM-DD-vN-rationale.md`

The rationale answers:
- What evidence prompted this change?
- What did the prior version get wrong?
- What's the hypothesis the new version is testing?
- What would falsify it?

This separates the *why* (here) from the *what* (the code/config diff). Reading these in order tells the story of how the tool's judgment evolved.

If your tool doesn't iterate on a versioned config, you can delete this directory.
