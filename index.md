---
title: Claude Code Setup Review
---

# Claude Code Setup: Examples From My Own Configuration


I use Claude Code every day. This page shows five parts of my own setup. Each part solves one problem that small teams meet when they adopt Claude Code. Every example here is in use now. I have used Claude Code for more than a year.

## What I Do

I help small software teams (5 to 30 people) get a Claude Code setup that works. This includes:

- A `CLAUDE.md` that tells the agent your rules once, so you do not repeat them in every session.
- Permission rules that let the agent work without a prompt for safe commands, and stop it for unsafe ones.
- Reusable agents, commands, and skills for the work your team does every week.
- A usage baseline, so you know what each developer spends and where the caps are.

I start with a fixed-price diagnostic. See [diagnostic.html](diagnostic.html).

## Example 1: Install Guardrails in `CLAUDE.md`

**Problem.** An agent that can run shell commands will install tools. Without rules, it uses `sudo`, `pip install` into the system Python, `npm install -g`, or `curl | bash`. After a week, the developer's machine is in an unknown state.

**How I use it.** My global `CLAUDE.md` has one section for installation. It has three parts:

1. Pre-flight rules. Check with `which <tool>` or `<tool> --version` before any install. Never use `sudo`. Never edit shell config files.
2. One tool per ecosystem. System tools use `brew`. Python uses `uv`. Node uses `nvm` and `npm`. Docker is present, never reinstall it.
3. A short list of forbidden commands. The list names each pattern, for example `pip install`, `npm install -g`, and pipe-to-shell installs.

The same file has a table of what is already installed, with versions. The agent reads the table and does not install what is there.

**Effect.** New sessions start with the same rules, with no need to explain them again.

## Example 2: A Permission Policy That Matches the Rules

**Problem.** Claude Code asks for permission on each command class until you set a policy. Teams answer "yes" to everything to stop the prompts. That removes the safety of the prompt.

**How I use it.** I keep three lists in `CLAUDE.md`, and the same lists in the settings file:

- Pre-approved, no prompt: read-only git commands, `git commit`, package manager run and test commands, `docker ps` and `docker logs`, and common file tools.
- Always denied: `sudo`, `rm -rf /`, `git push --force`, `git reset --hard`, `git clean -f`, global package installs, and pipe-to-shell installs.
- Still prompt: `git push`, `brew install`, `rm`, `docker run`, and `docker exec`.

**Effect.** Safe commands run without a prompt. The commands that can lose data still stop and wait for a human.

## Example 3: A House Writing Standard as an Output Style

**Problem.** Agent output is long, uses many synonyms for one concept, and writes vague phrases such as "some settings" or "may fail". Docs, commit messages, and error messages come out in a different style each time.

**How I use it.** I wrote one output style file. It sets rules for every document, comment, commit message, and error message the agent writes. Some of the rules:

- One term for one concept. The file has a table of the word to use and the words to avoid.
- One action per sentence. Sentence length limits for steps and for explanations.
- A list of forbidden vague phrases.
- Error messages have three parts: what happened, why, and what the user does next.
- A self-check list the agent runs before it sends output.

The same file has a section for chat replies: short, plain, only the necessary content, at most four options when a decision is needed.

**Effect.** Every document, commit message, and error message follows the same rules, in every session.

## Example 4: A Build-and-Test Verifier Agent

**Problem.** Before a deploy, someone runs lint, build, tests, and a diff check. When a person does this, steps get skipped. When an agent does this without a fixed order, it reports "all good" after a partial check.

**How I use it.** One agent file defines a QA role with four steps in a fixed order. The agent stops at the first failed step:

1. Static checks: linter and type errors.
2. Build: the project build command, no warnings.
3. Tests: full suite, with a count of passed, failed, and skipped tests.
4. Change analysis: list changed files from `git diff`, and check for sensitive files such as `.env` or credentials.

The output format is fixed. Each step gets a pass or fail line, and the last line is "deployable" or "not deployable" with a reason.

**Effect.** The pre-deploy check is the same every time, and a partial check cannot report success.

## Example 5: A Code Review Agent With a Fixed Rubric

**Problem.** Review quality changes with the reviewer's mood and with the prompt. AI-written code often gets a lighter review than human-written code.

**How I use it.** One agent file defines a reviewer that does not write code. It checks six things on every review: correctness, security, performance, readability, consistency with the project style, and tests. It reports findings in one table, with file and line, a description, and a suggested fix. Each finding has one of three severity levels: must fix, should fix, or optional. The last line is one of three verdicts: merge, merge after changes, or redo.

A matching slash command runs the same rubric on the current `git diff` from inside a session.

**Effect.** Every review has the same shape. A new team member reads one table and knows what blocks the merge.

## Other Parts of the Setup

- Nine slash commands for daily tasks: commit and PR in one step with a sensitive-file guard, code review on the current diff, structured debugging, explain code, write tests, scan technical debt, safe refactor with a plan first, a git status summary, and a batch import of saved web clips into a notes wiki.
- Six agents with one role each: architect, mentor, reviewer, security audit, simplifier, and verifier.
- A task review skill that runs a five-step process on finished work: question each requirement, delete, simplify, speed up, then automate.
- A rule that every commit message uses one language and one prefix format, so the git log is uniform.

## Contact

<form action="https://formspree.io/f/FORMSPREE_ID" method="POST">
  <p><label>Your email<br><input type="email" name="email" required style="width:100%;max-width:420px"></label></p>
  <p><label>Team size and your Claude plan<br><input type="text" name="team" style="width:100%;max-width:420px"></label></p>
  <p><label>What do you want to fix?<br><textarea name="message" rows="5" required style="width:100%;max-width:420px"></textarea></label></p>
  <p><button type="submit">Send</button></p>
</form>

Fixed-price diagnostic (USD 300): [diagnostic.html](diagnostic.html)
