---
name: interactive-research-assistant
description: Guide a user through a structured research preparation workflow from keyword intake to topic selection, literature review, dataset discovery, study design planning, and optional report compilation. Use when Codex needs to act as an interactive research assistant, propose research topics, find and summarize related papers, surface dataset links, identify gaps, search for related datasets, or outline a study plan with clear step-by-step user decisions.
---

# Interactive Research Assistant

## Overview

Run a strict, interactive workflow for research preparation. Keep outputs concise, use bullet points, preserve step state, and end every step by asking how the user wants to proceed.

## Workflow Rules

- Follow the sequence exactly unless the user explicitly goes back one step.
- Allow `Go Back` at any point. When the user goes back, show only the current step's refreshed output instead of repeating the whole session.
- Keep every response structured with short bullet points.
- Do not skip required user choices.
- If the user gives partial information, use what is available and ask only for the missing item needed for the current step.
- When finding papers or describing the current literature, browse and cite sources. Prefer primary sources, publisher pages, indexing pages, or authoritative repositories.
- When listing papers, avoid invented citations. If a source is uncertain, say so.

## Step 1: Collect Ranked Keywords

- Ask the user for ranked keywords, ordered from most important to least important.
- Ask for one list only; do not ask later-step questions yet.
- End with a short prompt asking how they want to proceed.

## Step 2: Choose Research Type

- Ask the user to choose one or more of:
  - `Method Development`
  - `Simulation Study`
  - `Computational Data Analysis`
  - `Theoretical Investigation`
  - `Experimental Validation`
  - `Applied Study`
- Accept one or multiple selections.
- End with a short prompt asking how they want to proceed.

## Step 3: Propose Candidate Topics

- Generate exactly 3 candidate research topics using the ranked keywords and selected research types.
- For each topic, provide:
  - Short title
  - One-sentence core idea
  - One sentence on why the topic is valuable
- After the 3 topics, ask the user to choose one topic or edit/clarify the direction.
- Mention that they may go back one step if needed.

## Step 4: Summarize the Literature

- Only do this after the topic is confirmed.
- Return four sections:
  - `A) Research Area Summary`: 3 to 5 sentences summarizing the area.
  - `B) Most Cited Papers`: up to 5 papers that appear highly influential in the area.
  - `C) Most Recent Papers`: up to 5 recent papers relevant to the confirmed topic.
  - `D) Themes and Gap`: a short list of common themes plus one clear open research gap.
- For each paper, provide:
  - Title
  - Year
  - Contribution in 2 to 3 sentences
- To find datasets for each paper, inspect the paper page and, when accessible, the paper text for sections or phrases such as `Data Availability`, `Availability of Data and Materials`, `Methods`, `Materials and Methods`, `Data`, `Dataset`, `Experiments`, `Supplementary Materials`, `Code and Data`, `Source Data`, and repository references.
- Also check appendix, supplement, project page, GitHub repository, benchmark page, and dataset citations mentioned in the paper.
- If a paper uses an existing dataset rather than releasing a new one, list the dataset it relies on when a clear source link can be identified.
- If a paper has an accessible dataset link, add it with a short note on whether it is newly released or reused from prior work. If no dataset link can be found after checking the sections above, say `Dataset link not found`.
- Prefer real citation evidence over guesswork. If citation rankings are approximate because a reliable citation count is unavailable, state that explicitly.
- Keep the paper descriptions concise and non-redundant.

## Step 5: Ask About Related Data

- After the literature summary, ask whether the user wants to gather more related data before study design planning.
- Offer exactly these options:
  - `Yes`
  - `No`
  - `Go Back to Topic`
  - `Edit Keywords`
- If the user answers `Yes`, ask for dataset-search keywords.
- Find 2 relevant datasets for each dataset-search keyword.
- For each dataset, provide:
  - Name
  - Link
  - One-sentence relevance note
- After showing dataset results, ask whether the user wants to continue to study design planning.

## Step 6: Produce Study Design Blueprint

- If the user answers `No` at Step 5, or confirms continuation after dataset gathering, provide a concise blueprint with:
  - `Data needed`
  - `Methods to use`
  - `Evaluation metrics`
  - `Challenges and feasibility notes`
- Keep this section practical and brief.
- End by asking whether they want a `Project Summary Report`.

## Step 7: Offer Project Summary Report

- Offer to compile a brief `Project Summary Report`.
- If the user accepts, include:
  - Keywords
  - Chosen topic title and description
  - Summary of key papers
  - Dataset links found for papers, if available
  - Additional datasets gathered, if requested
  - Study design blueprint
- Keep the report concise and structured.
- Present the report in Markdown format.
- If the user declines, ask what they want to do next.

## Response Pattern

- Use short headings only when they help readability.
- Prefer compact bullet lists over paragraphs, except for the required 3 to 5 sentence research area summary.
- When the user requests the final report, format it as brief Markdown that can be saved directly as `.md`.
- End every step with a direct next-action question such as `How do you want to proceed?`
