# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall accuracy

The fine-tuned TakeMeter model achieves at least 65% overall accuracy on the held-out Hacker News test set in each of the three Unit 6 runs.

**Why this target:** TakeMeter must distinguish technical explanations, personal experiences, and unsupported opinions. These categories sometimes overlap, so 65% represents a meaningful improvement over approximately 33% accuracy from random guessing on a balanced three-label dataset while accounting for our relatively small dataset.

---

## 2. Technical explanation F1

The model achieves an F1 score of at least 0.60 for `technical_explanation` on the held-out test set in each of the three Unit 6 runs.

**Why this target:** Technical explanations can overlap with unsupported opinions when commenters make technical claims without providing evidence. An F1 score of 0.60 would indicate reasonable precision and recall despite this ambiguity.

---

## 3. Personal experience F1

The model achieves an F1 score of at least 0.60 for `personal_experience` on the held-out test set in each of the three Unit 6 runs.

**Why this target:** Some Hacker News comments combine firsthand experiences with broader judgments, particularly in discussions about hiring and developer tools. This target tests whether the model can recognize personal accounts without relying only on obvious first-person wording.

---

## 4. Dataset balance

No single label accounts for more than 60% of the completed `labels.csv` dataset.

**Why this target:** Hacker News discussions may contain more technical explanations and opinions than personal experiences. Limiting any single category to 60% reduces the risk of training a classifier that favors the most common label while still allowing realistic differences in category frequency.

---

## 5. Labeling consistency

Two independent labeling passes on the same 20 Hacker News comments achieve at least 80% exact agreement, equivalent to 16 or more matching labels out of 20.

**Why this target:** Our distinction between technical explanations and unsupported opinions requires judgment about whether a comment provides checkable supporting details. Relabeling 20 comments independently will help assess whether our taxonomy produces consistent decisions rather than depending on a single interpretation.



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
