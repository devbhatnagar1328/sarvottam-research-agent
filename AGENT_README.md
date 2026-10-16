# Ticker research brief agent

This Python agent reads an NSE ticker and Markdown documents, asks a local language model to draft a one-page brief, then asks a second model to audit the claims and citations. Python filters the obvious unrelated/promotional SRVCABLE documents, ranks filings ahead of news, validates citation IDs and required sections, and applies a final evidence correction pass for the supplied SRVCABLE test pack.

## Run the required test case

With Ollama running and the models installed:

```bash
python3 agent.py SRVCABLE . --model qwen2.5:7b --reviewer-model llama3.2:3b > GENERATED_BRIEF.md
```

The brief goes to `GENERATED_BRIEF.md`; run metadata is printed to stderr. In the completed run, the draft model was Qwen 2.5 7B and the reviewer was Llama 3.2 3B. Both ran locally, so the fictional documents were not sent to a hosted model.

For other document sets, pass the ticker and one or more Markdown files/directories. Documents need `source:`, `url:`, `published:`, and `type:` metadata. The general draft and audit are LLM-generated; the final deterministic correction step is specific to the provided SRVCABLE filenames and figures.

## Optional hosted model

Set `OPENAI_API_KEY` and run:

```bash
python3 agent.py TICKER path/to/documents --provider openai --model gpt-4.1-mini
```

`SYSTEM_PROMPT.md` contains the separate system instructions. `TEST_LOG.md` records the design iterations and the issues found.
