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

I'm a student in Code Path's AI301 course, new to contributing to open source and interested in data work. In this repo I reproduce bugs and report exactly what I found.

## Rules I write by

### Rule: Promise the investigation, not the fix

I only commit to reproducing the issue and reporting back. No fix until I know more.

- Wrong: "I'll have a fix up completed soon."
- Right: "I'm going to reproduce this locally and post what I find here."

### Rule: Name this issue's details

Every comment mentions something specific to this issue, like the file, the test, or the error, so it couldn't be pasted on any other issue.

- Wrong: "I'd like to work on this"
- Right: "I'd like to take #58. I'll start by running the 9 failing tests in tests/unit/test_bias_detector.py."

### Rule: Show, don't claim

If I say something happened, the output is in the comment. If I think I know the cause, I call it a guess.

- Wrong: "It's broken because the regex is wrong."
- Right: "All 9 tests fail with the output below. My guess is the patterns are too narrow, but I haven't confirmed that."

### Rule: Say it plainly when it doesn't reproduce

A cannot-reproduce is a real result. I report it with what I ran instead of hiding it or forcing a match.

- Wrong: "Seems to work fine now?"
- Right: "I couldn't reproduce this. I ran the steps below on Windows 11 with Python 3.10, and all tests passed. Output attached."
## Things I never post

- "+1", "same here", or "can confirm" with no evidence of my own
- A promised fix, PR, or deadline in a claim comment
- A cause stated as fact without output to back it
- A repro copied from a classmate's comment
- A comment that skips AI-use disclosure when the repo's policy asks for it

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
