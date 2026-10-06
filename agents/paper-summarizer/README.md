# Paper Summarizer

Turns papers into structured summaries you can trust: the problem, the approach, the real numbers, the limitations, and why it matters for your topic. Give it several papers and it adds a comparison table and a short synthesis.

## What it needs

**Working folder:** every agent has its own, and this one's is `~/.nest/local/work/paper-summarizer/` on your computer (`%USERPROFILE%\.nest\local\work\paper-summarizer\` on Windows). The agent sees it as its current directory, so a path like `./notes/` means `~/.nest/local/work/paper-summarizer/notes/`. Other agents can't see this folder; in workflows, results pass between agents in their replies.

- PDFs or text files in `~/.nest/local/work/paper-summarizer/papers/`, or text pasted into chat. In the Literature Review workflow it receives ArXiv Researcher's shortlist (with abstracts) in the message and uses any matching PDFs from its own `papers/` folder.
- PDF text extraction uses `pdftotext` when the runtime image has it, otherwise a Python PDF library if one is installed. Scanned PDFs without a text layer can't be read; the agent tells you instead of guessing.
- No internet access. It never downloads papers.

## What it produces

- `./summaries/<paper-slug>.md` for each paper, plus `./summaries/index.md` for multi-paper runs.
- A short version in chat: one TL;DR per paper and the synthesis.

## Example prompts

- "Summarize every PDF in ./papers and tell me which two to read first."
- "Compare the three papers in ./papers on evaluation methodology."
- "Summarize this abstract for a product manager: <paste>"
- "What are the limitations of the paper in ./papers/longrope.pdf? Quote the authors where you can."

## Capabilities in plain language

| Capability                       | Why                                                                     |
| -------------------------------- | ----------------------------------------------------------------------- |
| Runs shell commands (asks first) | Extracts text from PDFs (`pdftotext` or Python) and searches long texts |
| Reads files and lists folders    | Finds and reads your papers                                             |
| Writes files (asks first)        | Saves summaries to `./summaries/`                                       |
| Network                          | None                                                                    |

Summaries only state what the paper says. The agent's own observations are labelled "Reader note".
