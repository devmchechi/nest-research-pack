# Citation Formatter

Turns DOIs, arXiv IDs, titles or a messy pasted reference list into clean BibTeX, APA 7 and MLA 9 citations. It checks every reference against Crossref or arXiv, fixes wrong years and misspelled names, points out preprints that have since been published, and tells you which entries it could not verify.

## What it needs

**Working folder:** every agent has its own, and this one's is `~/.nest/local/work/citation-formatter/` on your computer (`%USERPROFILE%\.nest\local\work\citation-formatter\` on Windows). The agent sees it as its current directory, so a path like `./notes/` means `~/.nest/local/work/citation-formatter/notes/`. Other agents can't see this folder; in workflows, results pass between agents in their replies.

- Identifiers or references in chat (in the Literature Review workflow, ArXiv Researcher's shortlist), or files in `~/.nest/local/work/citation-formatter/`: an existing `.bib`, a JSON shortlist, or a text list.
- Optional: add your email to `instructions.md` so Crossref puts your requests in its faster "polite pool".

## What it produces

- `./literature/references.bib` and `./literature/references.md` (APA and MLA). Existing files are merged, never wiped.
- A verification report listing each entry as verified or unverified, with the reason.

## Example prompts

- "BibTeX for 10.18653/v1/N19-1423 and arXiv 1706.03762."
- "Clean up this reference list into APA 7: <paste>"
- "Make citations for every paper in this shortlist: <paste ArXiv Researcher's JSON block>"
- "Check my refs.bib for wrong years and missing DOIs."

## Capabilities in plain language

| Capability                                      | Why                                                     |
| ----------------------------------------------- | ------------------------------------------------------- |
| Runs shell commands (asks first)                | Looks up metadata with `curl` and parses it with Python |
| Reads files and lists folders                   | Reads your existing reference files                     |
| Writes files (asks first)                       | Saves `.bib` and Markdown reference files               |
| Network: `api.crossref.org`, `export.arxiv.org` | Metadata lookups. Every other host is blocked.          |

It never makes up a DOI, volume or page range. Missing fields are left out and flagged.
