# Research Pack

Find, read and cite research papers with three agents that hand work to each other: one searches arXiv and Semantic Scholar, one writes faithful structured summaries, and one produces verified citations. The **Literature Review** workflow chains them into a cited review in one run.

## Agents

| Agent                                                     | What it does                                                                                          | Network                                       |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| [ArXiv Researcher](agents/arxiv-researcher/README.md)     | Searches arXiv and Semantic Scholar, ranks by relevance, citations and recency, and saves a shortlist | `export.arxiv.org`, `api.semanticscholar.org` |
| [Paper Summarizer](agents/paper-summarizer/README.md)     | Structured summaries of PDFs, text or abstracts, plus comparisons and syntheses                       | none                                          |
| [Citation Formatter](agents/citation-formatter/README.md) | Verified BibTeX, APA 7 and MLA 9 from DOIs, arXiv IDs or messy references                             | `api.crossref.org`, `export.arxiv.org`        |

## Workflow: Literature Review

`workflows/literature-review.yaml` runs four steps on the standing topic in ArXiv Researcher's `instructions.md`:

1. **search** (ArXiv Researcher): a ranked shortlist, ending with the full shortlist as JSON in its reply.
2. **summarize** (Paper Summarizer): one summary per paper from that JSON. It uses full-text PDFs from its own `papers/` folder when you've added them (`~/.nest/local/work/paper-summarizer/papers/`), otherwise the abstracts.
3. **cite** (Citation Formatter): BibTeX plus APA and MLA for the same shortlist, returned in its reply. If this step fails, the workflow continues without it.
4. **synthesize** (Paper Summarizer, pauses for your approval): the final review, with a thematic synthesis, a comparison table, open problems and references. It is returned in the reply and saved to `~/.nest/local/work/paper-summarizer/literature/review.md`.

Before running it, fork ArXiv Researcher and set your topic in its `instructions.md`.

## Working folders

Every agent has its own working folder, `~/.nest/local/work/<agent-id>/` on your computer (`%USERPROFILE%\.nest\local\work\<agent-id>\` on Windows), which it sees as its current directory. Agents can't see each other's folders. Put input files in the folder of the agent that reads them; in workflows, results pass from step to step in the agents' replies, never through files.

## Capabilities

- **Tools:** shell commands, reading and writing files, listing folders. Shell commands and file writes always ask for your approval first.
- **Network:** only `export.arxiv.org`, `api.semanticscholar.org` and `api.crossref.org`. Paper Summarizer has no network access.
- **Pilots:** none.
- **Typical cost:** about $0.05 to $0.60 per Literature Review run on paid models, depending on the shortlist size and whether full-text PDFs are summarized.

## Fork to customize

Installed agents are read-only so updates stay clean. To change a topic, style or default, **fork** the agent in Nest. You get your own editable copy and keep the original's behavior as a starting point. Each agent's `instructions.md` holds its user-editable defaults, marked "Edit me after forking".

## License

MIT. See [LICENSE](LICENSE).
