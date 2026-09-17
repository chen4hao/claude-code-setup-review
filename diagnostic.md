---
title: Claude Code Diagnostic
---

# Claude Code Diagnostic


**Price: USD 300, fixed.**
**Delivery: a written report in 5 business days after I receive your files.**

## Who This Is For

- A software team of 5 to 30 people.
- You pay for Claude Code today (Pro, Max, Team, or API).
- Your team uses it, but the results are uneven. Some people get value, some do not.
- You do not have a baseline for what each developer spends, or what they get for it.

## What You Get

1. **A written report** (PDF or Markdown) with a health check and a ranked fix list for six areas:
   - `CLAUDE.md`: what it tells the agent, what is missing, what is wrong.
   - Skills and commands: which ones exist, which ones your team repeats by hand.
   - Hooks: which events run a script, and which should.
   - Permissions: what runs without a prompt, what is denied, what still asks.
   - Usage and caps: what each developer spends per month, where the plan caps are, and where sessions hit them.
   - Memory and project files: what the agent remembers between sessions.
2. **A fix list.** Each item has a priority, the change to make, and the reason. Items you can do in one hour are marked.
3. **Three ready-to-use files** from the fix list: an updated `CLAUDE.md`, one permission policy, and one agent or skill for your most repeated task.
4. **Written Q&A by email** for 14 days after delivery. Ask anything in the report; I answer within one working day.

## What I Look At

You send me these files. Remove secrets before you send them.

- Your `CLAUDE.md` files (global and project).
- Your `.claude/` folder: agents, commands, skills, hooks, settings.
- One or two real session transcripts, or a description of a task that went badly.
- Your Claude plan type and the number of seats.
- Answers to a short intake form (10 questions, 15 minutes).

You can share a private repo, a zip file, or paste the files. I do not need access to your production code.

## Process

1. You pay the invoice. See "Payment" below.
2. I send the intake form. You return it with your files.
3. I review the files and write the report. This takes 5 business days.
4. I send the report and the three files.
5. You ask questions by email for 14 days after delivery.

## Examples of Findings

These are the kinds of items the report contains. They come from my own setup and from the public Claude Code documentation.

- The permission policy allows every command, so the agent runs `git push --force` without a prompt.
- `CLAUDE.md` is 400 lines and the agent ignores the rules at the end. Split it, and move project rules to the project file.
- The team re-explains the same coding conventions in every session. One `CLAUDE.md` section replaces that.
- Sessions hit the 5-hour usage cap in the middle of a task. A common cause is a loop of sub-agents that a single command could replace. I have hit this cap myself.
- A "verify before deploy" step exists as a checklist in a wiki. Nobody runs it. One agent file runs it the same way every time.

## What Is Not Included

- I do not write your production code.
- I do not change your Anthropic plan, seats, or billing.
- I do not run a security audit of your codebase.
- I do not promise a specific cost reduction. The report gives you a baseline and a fix list. The result depends on what you change.
- I do not share your files with anyone, and I delete them 30 days after delivery.

## Next Steps After the Diagnostic

- **Implementation.** I apply the fix list with your team, and build the agents, skills, and hooks in the report. Price: from USD 800, fixed quote after the diagnostic.
- **Monthly maintenance.** I review usage and update the setup each month. Price: from USD 150 per month.

Both are optional. The diagnostic has value on its own.

## Payment

I invoice through Payoneer.

1. You send me your company name, billing email, and country.
2. I create a payment request in Payoneer. You get an email with a link.
3. You pay by bank transfer (no fee) or by credit card (Payoneer charges up to 3.99%; you choose who pays it at checkout).
4. I start the work when the payment clears. I send the intake form the same day.

I do not start before payment. If you cancel before I send the intake form, I refund the full amount by a Payoneer payment to you within 3 business days. After that, there is no refund, because the review work has started.

## Contact

<form action="https://formspree.io/f/xdekoggp" method="POST">
  <p><label>Your email<br><input type="email" name="email" required style="width:100%;max-width:420px"></label></p>
  <p><label>Team size and your Claude plan<br><input type="text" name="team" style="width:100%;max-width:420px"></label></p>
  <p><label>What do you want to fix?<br><textarea name="message" rows="5" required style="width:100%;max-width:420px"></textarea></label></p>
  <p><button type="submit">Send</button></p>
</form>

My own setup, with examples: [index.html](index.html)
