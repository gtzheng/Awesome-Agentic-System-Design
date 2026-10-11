# Contributing

[Home](README.md) · [Updates](UPDATES.md)

Help readers understand a design decision. A short, well-explained addition is more useful than a large collection of unannotated links.

## What belongs here

- Primary research with a clear relationship to agent architecture, context, tools, coordination, evaluation, safety, or operation.
- Official specifications and project documentation explaining concrete interfaces or behavior.
- Engineering reports that expose mechanisms, constraints, failure modes, or measured tradeoffs.
- Learning material, exercises, and interview cases that teach transferable design reasoning.

Avoid unsupported performance claims, generic marketing, duplicate links, affiliate/tracking parameters, and tools with no explanation of their system design relevance.

## Where an addition goes

| Content | Location |
| --- | --- |
| Learning sequence or design explanation | [Topic guides](README.md#core-topics) |
| Interview exercise or worked design | [Interview guide](docs/interview-preparation.md) or [case studies](docs/case-studies.md) |
| Book, tutorial, specification, engineering report | [Guides](resources/guides.md) |
| Research paper | [Papers](resources/papers.md) |
| Framework, SDK, runtime, application example | [Frameworks](resources/frameworks.md), in the appropriate category |
| Release, deprecation, important paper, or changed assumption | [Updates](UPDATES.md), plus the affected catalog/guide |

## Minimum information

For a resource, provide the title, author/project, canonical URL, type, and one sentence explaining its design relevance. For papers, use an abstract or publisher page with version history and distinguish the first submission from later revisions. For software, check current maintenance status and avoid importing unsupported claims from promotional descriptions.

For an update entry, use:

```text
Event/publication date:
Title and primary source:
Status: released / preview / deprecated / roadmap / research
What changed:
Design implication:
```

Do not infer publication dates from search-engine crawl dates. Label a proposal as a proposal. Keep performance numbers only when their dataset, split, model/runtime versions, budget, and source are given. State whether reproduction is available or has actually been performed.

## Writing style

Use direct descriptions and concrete terms, such as retry limits, execution limits, and clearly defined tasks. Resource tables use descriptive labels such as **Topic**, **Coverage**, and **Focus**.

Learning paths describe topic sequences and prerequisites. Examples and design questions support exploration at the reader's own pace. Keep content pages focused on the material and its concepts. Record source-verification details and repository maintenance notes in pull request discussions.

## Review checklist

1. Open the source and confirm that the title, description, and status match its contents.
2. Prefer the author's repository, official documentation, publisher, or paper. If access requires registration or purchase, say so.
3. Check for an existing entry and update it rather than duplicating it.
4. Use repository-relative Markdown links for local navigation. Confirm files, heading anchors, and image paths resolve.
5. Check tables and Mermaid diagrams in a Markdown preview. Keep examples and numerical assumptions explicitly labeled.
6. Run `git diff --check` and review the diff for accidental removals or unrelated changes.

Submit a pull request explaining what the addition helps a reader learn and how you checked it. Disclose an affiliation with a submitted project where relevant.

## Freshness policy

At each editorial pass, prioritize broken or redirected links, deprecations, renamed projects, protocol changes, and research that changes a design assumption. Distinguish concepts that remain useful from APIs that have aged. Preserve useful historical material with a status note.

Investigate failed requests, including possible access restrictions, before removing a resource. Record unresolved verification limits in the pull request discussion. Git history records repository changes.
