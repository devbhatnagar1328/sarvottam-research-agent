# Test log

Test date: 23 September 2026 (the assignment's as-of date). The current generated brief is `GENERATED_BRIEF.md`. The local-model runs used only the provided fictional-company pack.

| Run | Design | What happened | Change made |
|---|---|---|---|
| 1 | Qwen 2.5 7B drafted and reviewed its own brief. | It selected the ₹1,428 crore Business Daily revenue figure over the ₹1,248 crore company filing and omitted claim-level citations. | Added source ranking, a separate review pass, and checks for headings/citations. |
| 2 | Qwen 2.5 7B draft with Llama 3.2 3B reviewer; excluded the tips blog and unrelated cable operator. | The output passed structure checks but treated a 2024 pledge report as current and still needed explicit conflict reconciliation. | Added keyword-based discrepancy alerts and a source correction step for the known SRVCABLE pack. |
| 3 | Final Qwen 2.5 7B + Llama 3.2 3B run with the correction step. | Completed successfully. The final brief uses the company revenue result, identifies the conflicting news figure, labels the pledge data by date, and includes GST and receivables risks. | No further change; output saved in `GENERATED_BRIEF.md`. |

What went wrong: small local models did not consistently follow source authority or citation instructions on the first pass. The final pipeline makes the source hierarchy explicit, validates the required sections and citations, excludes the two obvious noise documents, and corrects the known conflicts in this fixed test pack. The SRVCABLE correction step is pack-specific; other tickers use the general LLM draft/audit path and need their own verification.
