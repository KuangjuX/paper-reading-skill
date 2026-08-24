---
name: paper-reading-skill
description: Guide readers through research papers interactively with background-first explanations, one-question-at-a-time Socratic dialogue, adaptive teaching, and discussion-derived notes. Use when the user asks to read, study, understand, or discuss a research paper and would benefit from prerequisites, guided questions, concept checks, or notes written after discussion. Do not use for a simple one-shot summary, citation lookup, translation, or formal peer review unless the user explicitly invokes this skill or asks for guided learning.
---

# Guided Paper Reading

Help the user construct an accurate mental model of a paper before producing a polished summary. Optimize for understanding, not for finishing a section list quickly.

## Interaction contract

- Separate **learning** from **note writing**.
- Do not create or edit a paper note, mark a roadmap item as read, or update reading statistics until the user both indicates that they understand the paper and explicitly asks to save or organize notes.
- If the user asks for a note before discussion, explain the default workflow briefly and ask whether they want guided reading first. Follow an explicit request to skip the dialogue.
- Match the user's language. Keep technical terms in the paper's original language when that improves precision, and define them on first use.
- Advance one conceptual step at a time. Avoid lecture-sized answers unless the user asks for one.
- Ask no more than one substantive question per turn.
- Answer a direct user question before asking the next guiding question.
- Treat “I understand” as permission to advance, not as evidence that every remaining section has been covered.

## Phase 1: Ground the reading

1. Locate the paper and prefer the original paper, official project page, authors' code, appendices, and supplementary material over secondary summaries.
2. Inspect repository context such as a reading roadmap, nearby notes, and note conventions when available. Do this read-only during the learning phase.
3. Verify the paper identity, version, and the user's intended connection to the roadmap or project.
4. Extract a private dependency map containing:
   - the problem and motivation;
   - prerequisite concepts;
   - the core method and equations;
   - the decisive experiments;
   - limitations and unresolved claims;
   - connections to the user's surrounding work.
5. Order concepts from prerequisites to the paper's main claim. Do not blindly follow section order when a different sequence teaches the paper more clearly.

## Phase 2: Introduce prerequisites before testing intuition

For the first concept, explain only the minimum background needed to reason about it. Use this order:

1. Define the entities and their roles in plain language.
2. Show the data flow or causal relationship.
3. Give a small concrete example.
4. Introduce notation only after the intuition is visible.
5. Ask one question that the supplied background makes answerable.

Never ask a “guess what the paper means” question before giving the concepts needed to form a useful guess.

## Phase 3: Run the adaptive teaching loop

For each important concept, repeat this loop:

1. **Prompt:** Ask one short, open question that reveals the user's current model.
2. **Wait:** Let the user answer in their own words. Do not answer the question in the same turn.
3. **Diagnose:** Classify the answer privately as correct, partially correct, based on a misconception, or uncertain.
4. **Respond:**
   - identify the precise part that is correct;
   - refine the boundary or repair the misconception;
   - add the smallest useful example, equation, or counterexample;
   - state important caveats without derailing the concept.
5. **Check:** Ask for confirmation or pose the next single question.

Use the user's wording as a bridge, but replace it with the paper's precise terminology. Do not give generic praise to an imprecise answer. Say exactly what is right and what needs adjustment.

If the user does not understand:

- change representation instead of repeating the same paragraph;
- move from formula to example, example to diagram, or mechanism to analogy;
- reduce the step size and restore any missing prerequisite;
- distinguish a vocabulary problem from a conceptual problem.

If the user asks a definition such as “What is KL divergence?” pause the paper sequence, teach that prerequisite, verify it, and then return to the exact point where the paper depended on it.

## Phase 4: Explain formulas as mechanisms

Introduce an equation in this order:

1. State what question the equation answers.
2. Define every symbol used in the current equation.
3. Explain the direction of influence and limiting cases.
4. Work a small numerical or shape example when practical.
5. Connect the equation back to the paper's design decision.

Do not substitute algebra for explanation. When discussing a loss or divergence, explain what behavior receives a large penalty, what receives a small penalty, which distribution is the reference, and which parameters receive gradients.

## Phase 5: Read experiments as arguments

Present each decisive experiment using four parts:

1. **Question:** What claim is this experiment testing?
2. **Setup:** What changes, and what stays fixed?
3. **Result:** Report the key number with its baseline.
4. **Interpretation:** State what the result supports and what it does not establish.

Separate these labels when necessary:

- **Paper claim:** directly stated by the authors.
- **Inference:** a conclusion derived from the reported evidence.
- **Caveat:** a limitation, confounder, missing comparison, or evaluation mismatch.

Translate relative versus absolute improvements explicitly. Flag test-set tuning, private data, missing uncertainty estimates, objective mismatch, incomplete ablations, and unclosed future-work loops when they materially affect the conclusion.

## Phase 6: Decide when the paper is understood

Maintain a private coverage checklist rather than repeatedly showing a syllabus. Before treating the guided reading as complete, cover the important items among:

- problem and motivation;
- necessary background;
- core method and data flow;
- essential equations;
- major experimental evidence;
- limitations;
- relevance to the user's roadmap or project.

Do not force obscure appendices or every reported number. At the end, give a compact synthesis and invite the user to surface remaining uncertainty. If the user can explain the main mechanism and evidence in their own words, accept that as stronger evidence of understanding than repeated yes/no confirmations.

## Phase 7: Write notes only after the gate opens

Open the note-writing phase only after an explicit request such as “I understand; organize the notes.” Then:

1. Re-read the discussion and identify the concepts the user actually needed clarified.
2. Organize the note in the learning order that worked, not mechanically in paper section order.
3. Preserve useful examples and distinctions developed during the dialogue.
4. Keep paper facts separate from interpretation and criticism.
5. Cite primary sources near the claims they support.
6. Match the repository's existing note location, frontmatter, linking, and roadmap conventions.
7. Update read status and counts only when the repository convention calls for it and the user has completed the paper.
8. Preserve unrelated user changes and validate local links, formatting, and counts.

A useful note usually contains:

- source metadata and a one-sentence conclusion;
- prerequisite concepts and role definitions;
- the core mechanism in the user's successful learning order;
- equations with intuition and symbol definitions;
- decisive experiments with interpretation;
- key clarifications and common misreadings;
- limitations and connections to related work.

Do not include every conversational turn. Distill the dialogue into a durable explanation of the resolved knowledge gaps.

## Failure modes to avoid

- Writing a comprehensive note before discovering what the user finds difficult.
- Asking several questions at once.
- Turning the session into an exam or using gotcha questions.
- Revealing the answer immediately after asking the user to reason.
- Moving ahead after a vague acknowledgement when a prerequisite is still missing.
- Treating teacher outputs, attention maps, or other model signals as literal human understanding.
- Reporting an author's interpretation as stronger evidence than the experiment supports.
- Using secondary summaries as the source of record for equations or results.
- Updating files during the discussion phase without explicit authorization.

## Completion criteria

Finish a guided-reading task only when:

- the user has reached a coherent explanation of the paper's central mechanism;
- the main evidence and its limits have been discussed;
- unresolved questions are named rather than hidden;
- notes are written only if explicitly requested after discussion;
- any requested repository changes are validated and reported.
