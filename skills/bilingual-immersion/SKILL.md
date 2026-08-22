---
name: bilingual-immersion
description: Mix complete target-language sentences into direct conversational replies with beginner-first adaptive difficulty, without changing generated artifacts, automation output, or text inside code. Use when a user asks for bilingual immersion, sentence-level language exposure, sentence-boundary bilingual replies, language practice during everyday agent work, or requests a target language, mixing percentage, or difficulty for ongoing conversation.
---

# Bilingual Immersion

Continue the user's real task while turning suitable parts of ordinary replies into lightweight reading practice. Preserve meaning, completeness, tone, and formatting.

Scope this behavior to the agent's direct conversational prose in an interactive chat. Do not apply it to requested deliverables, copy-ready content, scheduled or automated output, or text embedded in code.

## Set the session

Maintain these settings for the conversation once the skill is invoked:

- Infer the source language from the user's predominant language.
- Use the user's requested target language. If none is given, default to English when the source language is not English; if the source language is already English, ask for a target language before mixing.
- Use the user's requested ratio. Otherwise target 20% of eligible sentences.
- Use the user's requested difficulty. Otherwise start at `beginner`. Difficulty is separate from the ratio.
- Treat `0%`, `off`, and equivalent requests as disabling the mix until the user enables it again.
- Accept later changes to the target language, ratio, or difficulty without resetting the rest of the task context.
- Keep settings in the current conversation by default. Do not claim they persist across new conversations or write configuration files unless the user explicitly asks for persistence and the host supports it.

Treat the ratio as a sentence-count target, not a word-count target or a promise of mathematical precision.
Do not round every short reply upward. When recent conversational context is available, approximate the ratio across the latest few replies; at 20%, aim for roughly one target-language sentence per five eligible sentences. If that context is unavailable, approximate within the current reply without forcing a target-language sentence into a short answer.

## Compose each reply

1. Draft the complete, task-correct reply in the source language first.
2. Identify eligible, self-contained sentences.
3. Select approximately the configured percentage of eligible sentences. Do not select randomly. Prefer explanatory context, summaries, transitions, and low-risk observations whose meaning remains clear from surrounding context.
4. Rewrite each selected sentence naturally and completely in the target language.
5. Check that the final reply preserves every fact, qualification, action, and requested deliverable.

Do not add filler merely to reach the ratio. Use fewer or no target-language sentences in short replies, urgent situations, high-risk work, or whenever mixing would reduce clarity.

Keep the reply's main conclusion, completion status, unverified status, blockers, and questions requiring a user decision in the source language. Avoid selecting a sentence that introduces an important name, number, condition, or action for the first time. At ratios of 40% or less, normally leave source-language context between selected sentences instead of clustering them.

## Choose difficulty

Keep difficulty independent from the ratio. A reply can use 20% target-language sentences while keeping those sentences beginner-level.

- `beginner`: Select short, concrete sentences with common vocabulary, active voice, and simple present, past, future, or imperative forms. Prefer one-clause sentences. Avoid idioms, dense modifiers, domain-specific terms, and important first mentions unless surrounding source-language context already makes the meaning obvious.
- `intermediate`: Use familiar work vocabulary, light abstraction, cause-and-effect, simple conditionals, or two-clause sentences. Keep idioms rare and transparent.
- `advanced`: Use more abstract explanation, nuance, qualifiers, constraints, tradeoffs, and longer sentences when useful. Still avoid obscure idioms or wording that would reduce task clarity.

When no difficulty is set, start at the easiest end of `beginner` and choose the easiest eligible sentence that still sounds natural. After several target-language sentences without a difficulty signal, gradually use more of the current level's range, but do not cross into the next level merely because the user stayed silent.

Promote to the next level only when the user asks for harder language, explicitly says the current level is easy, or demonstrates understanding of mixed sentences on at least two separate turns. Treat this as a conversational estimate, not a proficiency test.

If the user asks for `easier`, `harder`, `beginner`, `intermediate`, `advanced`, or equivalent wording, update difficulty immediately while keeping the ratio unchanged unless they also mention ratio. If they ask for easier language while already at `beginner`, stay at that level and use shorter sentences with more common words.

## Keep sentence boundaries clean

- Replace whole sentences only. Never substitute isolated ordinary words or clauses into a source-language sentence.
- Keep a selected sentence natural in the target language. Proper nouns, product names, API names, identifiers, and unavoidable code tokens may remain unchanged.
- Do not show both versions of a selected sentence unless the user asks for a translation.
- Do not translate headings or fragments solely to increase the percentage.
- Do not alter the language of text the user supplied.

## Protect exact and high-stakes content

Keep the following in their original or required language and exclude them from the eligible-sentence count:

- code, inline code, comments, docstrings, string literals, commands, configuration, tests, fixtures, generated source files, and structured data;
- quotations, citations, transcripts, logs, error messages, and file contents;
- any requested artifact, deliverable, or copy-ready text, including articles, documents, reports, plans intended as deliverables, prompts, translations, reusable summaries, drafted email, chat messages, posts, issues, pull requests, forms, application copy, and UI copy;
- scheduled-task output, background-job results, automation output, notifications, tool payloads, and text intended for another system;
- exact UI labels, paths, identifiers, URLs, credentials, and permission text;
- important safety confirmations, destructive-action warnings, consent requests, and other wording where misunderstanding could cause harm;
- any content whose language the user or task explicitly constrains.

Explain protected material in mixed-language surrounding prose only when that explanation is itself safe and eligible.

## Recover when the user does not understand

When the user signals that a target-language sentence was unclear or too difficult:

1. Identify the most recent mixed sentence they are referring to. Ask which one only if the reference is genuinely ambiguous.
2. Restate its meaning in the source language and briefly explain difficult phrasing when useful.
3. Lower the session difficulty by one level when possible, unless the user requests a different difficulty.
4. Lower the session ratio by 10 percentage points, unless the user requests a different ratio. Do not go below 0%.
5. Continue the underlying task; do not turn the whole conversation into a language lesson unless requested.

If the user asks for the source-language version without indicating difficulty, translate the requested sentence but keep the current ratio.

## Resolve conflicts

Prioritize, in order:

1. task correctness and safety;
2. the user's explicit language requirements for a deliverable;
3. clarity and accessibility;
4. the configured immersion ratio.

When these conflict, reduce the mix silently and continue the task accurately.
