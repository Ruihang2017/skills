# CLAUDE.md

Guidelines for proof-of-concept work. The job is answering one technical question with code — does this approach work, or doesn't it?

**The bias:** shortest path to a yes/no answer. Minimum UI only if it makes the concept easier to show; otherwise just a script that runs and shows the result.

## 1. Answer One Question

A PoC exists to settle a specific uncertainty. Name it before writing code.

- State the question in one sentence: "Can we extract structured fields from these PDFs with >90% accuracy?" "Does this rate-limited API support the volume we need?" "Will this algorithm converge on real data?"
- If the question isn't clear, ask. A PoC for the wrong question is wasted work.
- The output of the PoC is evidence for or against that question — printed numbers, a saved artifact, a passing/failing assertion. Nothing more.
- If you're tempted to add a second question, write a second PoC.

## 2. One File, Hardcoded Inputs

PoCs die when they grow scaffolding. Resist the urge.

- One script. One file if you can. Two only if a notebook plus a helper makes the result clearer.
- Hardcode inputs at the top. File paths, API keys via env var, sample data inline. No config files, no CLI flags, no argparse.
- No package layout. No `src/`, no `__init__.py`, no `setup.py`. Just `poc.py` (or `.ts`, `.ipynb`, etc.) at the repo root.
- Dependencies in a `requirements.txt` or single `package.json`. Whatever the language's lightest option is.

## 3. Show the Result, Loudly

The whole point is the result. Make it impossible to miss.

- Print the answer in plain English at the end: `"Accuracy: 94.2% (above 90% threshold — concept validated)"`, not a dict the reader has to interpret.
- If the result is a file (extracted data, generated output), save it to a named path and print where it went.
- If there are intermediate steps worth seeing, print them with labels. A wall of unlabeled numbers is not a result.
- For comparative PoCs (approach A vs B), print both side by side. The reader shouldn't have to scroll.

## 4. Skip Everything Else

If it isn't evidence for the question, it doesn't belong.

- No error handling beyond what's needed to not crash on the happy path. If the API returns 500, let it crash — that's a result.
- No retries, no exponential backoff, no graceful degradation. A PoC that hides failures is a PoC that lies.
- No tests. The script itself is the test.
- No abstractions, no classes, no dependency injection. Top-to-bottom procedural code is fine and often clearer.
- No logging framework. `print()` is the logging framework.
- No CLI flags, no API endpoint, no service. If someone needs to run it, they run the script.
- A minimum UI is fine *only* if the concept is hard to show without one — e.g., a single Gradio/Streamlit page, a one-file HTML, or a notebook with inline widgets. Pick the lightest option. No routing, no styling beyond defaults, no auth. If a `print()` would land the same point, skip the UI.

## 5. Be Honest About What Was Proven

PoCs lie most often by accident — by passing on data that's too clean, too small, or too cherry-picked.

- State the conditions under which the PoC ran: input size, sample source, any preprocessing. The result means nothing without them.
- If you used a smaller/simpler sample than production would see, say so explicitly: `// NOTE: tested on 50 records; production will see ~50k`.
- If a step is mocked or stubbed, mark it `// STUB:` and say what the real version would do.
- If the result is borderline, say it's borderline. Don't round up.

## 6. Surface the Next Question

A good PoC ends with the next decision teed up, not buried.

- After the result, state in a comment or printout what this implies: "Concept works on clean inputs; next risk is OCR'd PDFs." "Latency was 2.3s/call — too slow for inline use, fine for batch."
- If the answer is "no," say so plainly. A negative PoC is a successful PoC.
- Don't start building the real version inside the PoC. If the concept is validated, the next conversation is "what do we build now," not "let me keep extending this."

---

**Working signal:** running the script (or opening the one-page UI) answers the question in under a minute, the code is short enough to read in one sitting, and the next decision is obvious from the output.
