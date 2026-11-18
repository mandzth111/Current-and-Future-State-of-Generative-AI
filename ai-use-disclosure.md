# AI-Use Disclosure (Draft)

## Tools used

- **Claude (Anthropic)**, in the Claude app: planning, writing code, browser testing, and drafting documentation.
- **Replit**: hosting the running prototype.

## Development assistance

- **Problem framing:** Claude drafted the Problem Framing document from my capstone research, including my hand-built dataset of 32 Midwest cooperatives, and asked me questions to fill gaps instead of inventing evidence.
- **Code:** Claude wrote `index.html` (HTML, CSS, and JavaScript) for the First Working Slice and this revision: the quote check, fit rules, live rating, edit flags, and review lock.
- **Sample data:** Claude drafted the four fictional sample documents and the prepared (Wizard-of-Oz) results for each.
- **Testing:** Claude ran the test cases in a headless browser (Playwright) at desktop and phone widths, and took the before-and-after screenshots.
- **Writing:** Claude drafted the README, `revision.md`, and this disclosure, which I reviewed and edited.

## Representative prompts

1. **"Use Wizard-of-Oz prototype"** (First Working Slice). Claude's first version simulated the AI with keyword rules. I asked for a Wizard-of-Oz version instead. Claude rewrote it to show hand-prepared results for each sample, kept the quote check and fit rules as real code, and labeled what was simulated. This also fixed a bug in which the keyword rules counted newsletter "members" as meters.
2. **The revision assignment, my GitHub repo link, and my three peer reviews** (this milestone). Claude read the code, reproduced the reviewers' bug (an edited meter count still rated Match), proposed three priority changes, built them, and ran five test cases. I kept the scope to the review step and deferred connecting a live model.

## Human judgment

- **Rejected: keyword-rule simulation.** Claude's first prototype extracted facts with keyword rules. I rejected that approach because rules would look like a working AI feature while really being brittle pattern matching, and they misread members as meters. A Wizard-of-Oz version is more honest about what is simulated.
- **Deferred: connecting a live model now.** A reviewer recommended analyzing real documents. I chose to fix trust in the review step first, because the reviewers' evidence showed a copied profile could contradict itself, and a live model would only make that riskier.
- **Scope choices from my capstone research:** the target profile (distribution co-ops of 10,000 to 80,000 meters that run their own SCADA) and the five facts come from my interviews and dataset, not from AI.
- [ADD ONE MORE IN YOUR OWN WORDS: for example, a wording or design change you made after reading Claude's draft.]

## Verification

- Ran all five test cases in a browser and recorded the actual results, including the before-and-after comparison with the same input.
- Re-ran the reviewers' exact edits (5,000 and 120,000 meters) to confirm the rating now changes.
- Checked that every prepared quote appears word for word in its sample document; the quote check enforces this in code.
- Checked the layout at phone width (390 px) for cut-off text and horizontal scrolling.
- **Still needs checking:** how a real model performs on real documents, whether users read sources before confirming, and the fit thresholds against more of my capstone data.

## AI inside the product

| | |
| --- | --- |
| **Task** | Read public text about one electric utility and extract five facts: utility type, members or meters served, SCADA/OT ownership signals, named operations or IT leaders, and recent trigger events. |
| **Input** | Text the user pastes from one public document (annual report, newsletter, job posting, news page). |
| **Output** | A value and a supporting quote for each fact, or "Not found." Code then checks each quote against the input and rates fit with fixed rules. |
| **Current status** | **Simulated (Wizard-of-Oz).** Results for four fictional sample documents were prepared by hand. No model or API is connected. The quote check, fit rating, edit flags, and review lock are working code. |
| **Planned** | Connect a language model for the final project, instructed to report only what the text states, never infer security weaknesses, and keep members and meters separate. |
