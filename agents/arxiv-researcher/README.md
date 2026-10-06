# ArXiv Researcher

Finds the papers that matter for a research question. It searches arXiv and Semantic Scholar, drops duplicates and papers that only mention your topic in passing, ranks the rest by relevance, citations and recency, and saves a shortlist. Its reply ends with the full shortlist as JSON, which the Literature Review workflow passes to Paper Summarizer and Citation Formatter.

## What it needs

**Working folder:** every agent has its own, and this one's is `~/.nest/local/work/arxiv-researcher/` on your computer (`%USERPROFILE%\.nest\local\work\arxiv-researcher\` on Windows). The agent sees it as its current directory, so a path like `./notes/` means `~/.nest/local/work/arxiv-researcher/notes/`. Other agents can't see this folder; in workflows, results pass between agents in their replies.

- Nothing to set up. Edit `instructions.md` (after forking) to set your standing topic, categories, date window and shortlist size.
- Semantic Scholar is used without an API key, so it is sometimes rate-limited. The agent backs off and falls back to arXiv-only results when that happens, and tells you.

## What it produces

- A ranked table in chat: title, first author, year, citation count, and why each paper made the cut.
- `./literature/papers.json` with full metadata and abstracts for every paper on the shortlist, repeated as a JSON block at the end of the reply.

## Example prompts

- "Find the 8 most-cited papers from the last two years on speculative decoding."
- "Recent surveys on graph neural networks for drug discovery, please."
- "What has Yann LeCun's group posted on arXiv about world models since 2024?"
- "Search for benchmarks that evaluate LLM agents on software engineering tasks."

## Capabilities in plain language

| Capability                                             | Why                                                                                      |
| ------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
| Runs shell commands (asks first)                       | Calls the arXiv and Semantic Scholar APIs with `curl` and parses the results with Python |
| Reads files and lists folders                          | Checks earlier results in `./literature/`                                                |
| Writes files (asks first)                              | Saves `./literature/papers.json`                                                         |
| Network: `export.arxiv.org`, `api.semanticscholar.org` | The two search APIs. Every other host is blocked.                                        |

It never invents papers. Every result comes from an API response, and if a search finds nothing useful it says so.
