# Interactive Research Assistant

`interactive-research-assistant` is a Codex skill for structured research preparation. It guides a user from ranked keywords to topic selection, literature review, dataset discovery, study design, and a brief Markdown project report.

## Install

Copy the skill folder into your Codex skills directory:

```bash
cp -R interactive-research-assistant ~/.codex/skills/
```

Restart Codex after installing so the skill is loaded.

## Invoke

Use the skill explicitly in a prompt:

```text
Use $interactive-research-assistant to help me prepare a research plan.
```

Example:

```text
Use $interactive-research-assistant to help me explore multimodal learning for medical imaging.
```

## Workflow

The skill runs in a fixed sequence:

1. Ask for ranked keywords.
2. Ask for one or more research types.
3. Generate 3 candidate research topics.
4. Summarize the literature for the chosen topic.
5. Ask whether to gather more related datasets.
6. Produce a concise study design blueprint.
7. Offer a brief Markdown project summary report.

## What It Returns

- Topic ideas with short rationale.
- A research area summary.
- Up to 5 influential papers and up to 5 recent papers.
- Dataset links found from papers when available.
- Two additional datasets per dataset-search keyword if requested.
- A concise study design blueprint.
- A brief final report in Markdown format.

## Dataset Finding Behavior

When checking papers, the skill looks beyond obvious download links. It inspects places such as:

- `Data Availability`
- `Availability of Data and Materials`
- `Methods` or `Materials and Methods`
- `Data`, `Dataset`, `Experiments`
- `Supplementary Materials`
- `Code and Data`
- Appendices, project pages, GitHub repositories, and cited benchmark pages

If a paper reuses an existing dataset, the skill should report that dataset when a clear source link is available.

## Navigation

- Say `Go Back` to move back one step.
- Say `Go Back to Topic` after literature review to revisit topic choice.
- Say `Edit Keywords` to restart from the keyword direction without repeating all prior output.

## Example Session Start

```text
Use $interactive-research-assistant to help me prepare a research direction.

Keywords:
1. graph neural networks
2. molecular property prediction
3. uncertainty estimation
```

