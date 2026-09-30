# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

I'm a student making my first open-source contributions as part of a coursework assignment. I've reproduced the bug myself in my own environment and I'm learning the codebase as I go. Readers can expect specific observations tied to real artifacts, honest uncertainty when I don't know something yet, and no promises I haven't earned.

## Rules I write by

### Rule: Name the thing specifically

Say which behavior, which version, which command — not "this issue" or "the bug." The reader has no idea which of the twenty things in the thread I'm referring to unless I say it.

- Wrong: "I can reproduce this issue and would like to help fix it."
- Right: "Reproduced on lazygit 0.64.1: pressing `s` on an untracked file opens the stash-name prompt but creates no stash and shows no error."

### Rule: Claim only what the evidence shows

Don't state conclusions the artifacts don't support. If the artifact is ambiguous or if I haven't traced the root cause yet, say so rather than reaching for a diagnosis.

- Wrong: "I confirmed this is a race condition in the debounce logic."
- Right: "The popup closes with no message; `git stash list` shows nothing. I haven't traced why yet — I'll look at where the stash-name prompt decides to proceed."

### Rule: Match confidence to the attempt

An honest cannot-reproduce is useful to the maintainer. A confident claim backed by nothing is worse than silence.

- Wrong: "Same issue here, definitely a bug on all platforms."
- Right: "I couldn't reproduce on Ubuntu 24.04 with 0.64.1 — my steps may differ. Here's what I tried and what I observed: ..."

### Rule: State intent concretely

Say what part of the code I plan to look at or what change I plan to attempt, not that I "want to help" or "would love to contribute."

- Wrong: "I'd love to contribute to fixing this if no one is working on it!"
- Right: "Plan: find where the stash-name prompt decides to proceed and add a guard for the untracked-only case, or surface an error instead of a silent no-op."

### Rule: Don't promise timelines

I don't know how long understanding and fixing a bug will take. Promising a date I can't keep is worse than saying nothing about timing.

- Wrong: "I'll have a PR up by the weekend."
- Right: "I'll start by reading the stash-related code and post an update once I understand the trigger."

## Things I never post

- Timelines or delivery promises ("PR by Friday," "2-day fix," "I'll fix it this week")
- Root-cause assertions without shown evidence ("it's clearly a race condition," "I verified the bug is in X")
- Boilerplate openers or closers ("Great issue!", "Hope you guys fix it soon", "Thanks for maintaining this!")
- "Same here" or "+1" comments with no artifact and no new information
- Confident reproductions where my artifact shows a different symptom than the issue describes
