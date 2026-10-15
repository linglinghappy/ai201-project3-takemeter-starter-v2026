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

On the test split, `accuracy` is at least 0.60 in all three seeds of the
Unit 6 "before" run.

**Why this target:** I have four labels, so a random guess gets about 0.25.
Always guessing my most common label (probably `advice` or `hot_take`) gets
about 0.35 to 0.40. 0.60 is clearly better than both. My test split is only
about 30 posts, so I did not set it higher.

---

## 2. Per-label performance

In all three seeds of the Unit 6 "before" run, `hot_take`, `vent` and
`advice` each have a per-label F1 of at least 0.50. `backed` has a per-label
F1 of at least 0.40. If a label has 0 posts in a seed's test split, that
seed counts as a miss for that label.

**Why this target:** `backed` is my hardest label. It was rare on r/csMajors:
I found only 2 or 3 clear examples in the 50 comments I read. In my stress
test, all 4 of my mistakes involved `backed`. It will also have only about
5 posts in the test split, so its score will jump between seeds. That is why
its target is lower than the other three.

---

## 3. Balance

In the final `labels.csv`, every label has at least 30 posts, and no label
is more than 40% of all rows.

**Why this target:** 30 posts means about 5 land in the test split. With
fewer, the F1 for that label means almost nothing. On r/csMajors, `advice`
and `hot_take` are very common and `backed` is rare. Without a limit,
`backed` could end up tiny. If I am short, I will look for threads with data,
like application stats or salary comparisons.

---

## 4. Consistency

At least three days after labelling my 20 `cold` posts, I re-label them
without looking at my first labels. I save this as `relabel_check.csv` with
columns `text`, `first_label`, `second_label`, and write both dates at the
top of the README Dataset section. At least 16 of 20 rows have `first_label`
exactly equal to `second_label`.

**Why this target:** In my stress test, I broke my own rules on 4 of 10
posts. So I know labelling is not easy for me, and 100% is not realistic.
But if I agree with myself less than 80% of the time, the model gets a messy
signal. Then a low score would be my fault, not the model's.

---

## 5. Confidence

In all three seeds of the Unit 6 "before" run,
`accuracy_most_confident_third` minus `accuracy_least_confident_third` is
at least 0.15.

**Why this target:** Some of my posts are clear, like "150 apps, 0
interviews, it's over for me". Others sit on a boundary, like a personal
story that may or may not support the claim. The model should be more sure
on the clear ones. If being confident does not make it more accurate, its
confidence is useless to a reader. One risk: with about 30 test posts, each
third is only about 10 posts, so 0.15 is a gap of just 1 or 2 posts.

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
