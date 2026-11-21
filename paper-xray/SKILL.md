---
name: paper-xray
description: Turn a scientific paper into a structured, condensed HTML walkthrough: background, results grouped by message, one figure card at a time, and traceable sources. Use when asked to make a paper easier to read.
---

# Paper x-ray

Build a single self-contained HTML file that restructures a paper so it can be read in the order a reader actually needs: why the work was done, what to do with it, and what each figure shows.

## 1. Locate and read the paper

If the user gives a DOI, title or author, search their Zotero first (`zotero_search_items`; a DOI often fails substring match, so get the title from `bioRxiv get_preprint` or PubMed and search by first author). Confirm the item and its PDF attachment before building anything.

Read the whole text, not just the abstract: `zotero_get_item_fulltext` returns the first pages, then `zotero_read_pdf_pages` for the rest. **Read the figure legends** (usually a block after the Discussion) and the Extended Data legends. Note whether the PDF prints line numbers in the margin; preprints usually do, and they become the citation anchors.

## 2. Section isolation (the rule that matters most)

Each section of the guide draws **only** on the matching part of the paper:

| Guide section | Allowed source |
|---|---|
| Background | the Introduction only |
| Discussion | the Discussion only |
| Results | the Results text and the figure legends |

The abstract mixes all three, so it is not a source for any of them. This is easy to violate by accident: the Discussion often restates the Introduction's gap with sharper numbers, and each Results subsection opens with a motivating sentence that reads like background. Both are leaks. After drafting, grep each section for the other sections' signature terms and move anything misfiled.

## 3. Structure

**Background.** A field-level big question (the standing problem many papers work on, not this paper's aim), then "What was already known" as a short list drawn from the Introduction, then the specific questions this paper alone set out to answer. Each specific question carries a **Motivation** line saying what known thing made it worth asking. Do not add hypotheses unless the paper states them in the Introduction.

**Discussion.** Pairs of **Conclusion** and **Future directions**, so each recommendation sits beside the finding it rests on. Then a **Limitations** list. Drop generic recommendations that the paper does not support.

**Results.** Three nested levels:

1. One block per main message, titled from the paper's own section headers. Do not make these collapsible: the point is a walkthrough the reader can take in without clicking anything open.
2. A **Method** block under it as a numbered list of steps ("do X, keep the N that pass, cluster them, test enrichment").
3. Figure cards, **one visible at a time**, switched by a row of tag buttons under the method. Each card holds: the condensed caption, the question that figure answers, and the Main text that interprets it.

Each result block ends with a **Main message** summary.

Reference figures by ID (`Fig1a`, `FigS3d-i`); do not extract images unless asked. Place supplementary figures next to the main panels they support rather than dumping them at the end of the block.

Give every card header a short 1-3 word label: `Method · Response timing`, `Conclusion · Timing decoupled`.

## 4. Sourcing and attribution

Every claim gets a marker that opens its source. Two rules govern what the source says:

**Do not reproduce the paper's sentences.** Not in tooltips, not in a panel, not at scale anywhere. Use a **find anchor**: the first few words, an ellipsis, the last few words, with the substance elided, so the reader can Ctrl+F into their own PDF.

```
"Cardiac mesoderm emerged as a ... canalise mesoderm differentiation." · Discussion, lines 438-443
```

Keep each side to roughly three to six words. Where a sentence is short enough that head plus tail would hand over the whole thing, give the opening anchor and the line numbers only.

**Tag provenance.** Every entry is either:

- **Authors'** — the claim is theirs and the anchor lands on it.
- **Mine** — the statement is your inference, and the anchor points to the conclusion you drew it from, with a sentence saying what you inferred.

This matters most in Future directions. A paper that nominates two candidate genes has not thereby recommended testing them; writing "functionally test X and Y" in the authors' voice is the failure mode to avoid. Audit every recommendation and tag honestly. Never leave a claim with no entry at all.

## 5. Interaction

- A sticky jump bar across the top: chips for the non-Results sections, a dropdown for the result blocks that fills in with the current section as the reader scrolls, and a dropdown of every figure ID.
- Figure tags switch one card at a time. Label the first tag of a run in full (`Fig1a`) and drop the prefix on the rest (`1b`, `1c`).
- Source markers open a panel that slides up from the bottom of the window, with a close button, Escape, clicking the marker again, and clicking outside all closing it. Style it to match the page, not as a dark overlay.
- Jumping to a figure must reveal its tab first, or the link lands on a hidden card.
- Avoid a box inside a box: content inside an already-bordered card should be plain unless it needs separating.

## 6. Build and verify

Write one self-contained HTML file: markup, styles and script together, no external assets. For a document this size, generate or edit it with jsdom rather than a chain of regex replacements, which are fragile against nested markup.

Verify headlessly before delivering, with jsdom and `runScripts: 'dangerously'` (stub `scrollIntoView`, which jsdom lacks):

- every figure anchor unique, every dropdown option resolving to a real element
- every jump revealing a hidden tab rather than landing on a hidden card
- every marker opening the panel with non-empty content and a distinct title
- every card carrying its source entry, every future direction tagged stated or inferred
- no anchor exceeding the length rule
- tag counts balanced, script parsing with `node --check`

## Pitfalls

- Writing the guide from the abstract. It is the one part of the paper that cannot be used.
- Opening a format skill before gathering material; the layout then pulls the work toward empty templates.
- Attaching a source marker to the conclusion half of a pair and leaving the recommendation half bare, which reads as if the recommendation were invented.
- Mirroring the paper's own section order instead of grouping figures under the message they support.
- Regex edits with `{...}` delimiters in Perl breaking on CSS braces; use `s!...!...!` instead.