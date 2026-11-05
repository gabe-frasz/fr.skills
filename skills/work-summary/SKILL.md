---
name: work-summary
description: Generate a concise work summary from local Git history and GitHub pull requests for user-selected projects.
disable-model-invocation: false
compatibility: Requer Git e GitHub CLI (gh) autenticado, com acesso de leitura aos repositórios e pull requests analisados.
license: MIT
---

# Work Summary

Reconstruct the user's work from local Git history and GitHub pull-request activity, then return a publication-ready summary.

## Inputs

- Treat repository names and paths in the prompt as the project set.
- If the prompt does not identify any projects, ask which projects to analyze and wait for the answer before researching.
- Use the current local calendar day as the period by default. Change the period only when the user explicitly provides another date or range.
- Treat the research and output rules below as defaults. Follow any explicit user instruction about period, projects, scope, sources, content, language, length, audience, voice, or structure instead of the corresponding default.

## Research

For every selected project:

1. Resolve its local repository from the supplied path, the current workspace, or nearby project directories. If a project cannot be resolved unambiguously, ask for its path. Inspect repositories without changing files, branches, refs, or remote state.
2. Identify the user from the authenticated GitHub account and the repository's Git author configuration. Analyze the user's work rather than the whole team's activity unless the user explicitly requests a team summary.
3. Inspect all local Git refs within the exact period, including unpushed work. Exclude automatic checkpoints, bot activity, and commits that cannot be attributed to the user.
4. Inspect the repository's GitHub pull requests with `gh`. Count a pull request only when the user performed material activity within the period, such as opening it, adding commits, reviewing it, commenting substantively, triggering a meaningful workflow, or merging it. An automated timestamp change or base-branch update is not evidence of the user's work.
5. Cross-check commits and pull requests so the same work is described once. Use the changed behavior and pull-request context to determine the task's purpose and product outcome; keep inferences conservative and grounded in the evidence.
6. Arrange the confirmed work by when it happened. Prioritize user-facing changes and meaningful enabling work over incidental maintenance details.

If a required repository or GitHub source remains inaccessible, produce a partial summary. Do not include extra debug text on the summary.

## Default output

- Return only the summary, without a heading, bullet list, methodology, source list, or preamble.
- Write in Brazilian Portuguese, in the first person singular.
- Write at least two and at most four complete sentences.
- Keep the text brief, formal, descriptive, and chronologically ordered.
- State the product area or capability changed and the practical purpose or outcome of the work.
- Translate implementation details into language a Product Owner can understand. Omit code, file names, commit hashes, pull-request numbers, library names, internal data structures, and unexplained technical jargon.
- Start directly with the work performed; do not use “hoje” as an opening or time marker.
- Combine closely related commits and pull-request activity into one coherent task. Avoid repetition added only to reach the minimum sentence count.
- When no attributable work is confirmed, use two concise sentences to state that no activity was found and identify the projects and period checked.
