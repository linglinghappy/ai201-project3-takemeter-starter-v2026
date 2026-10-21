# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->



---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `backed`

**Definition:** A conclusion (a claim or a piece of advice) supported by evidence that directly explains why it's true, where evidence is either a specific, checkable fact from any source (a number, a rule, a study) or the writer's own first-hand experience.

**Example 1:**
> Do NOT ghost the loan management company. Call and tell them your situation, you’ll enter forbearance, WAY better than defaulting.
>
> If you’re in default, call anyways. Do not ghost the loan management company.
>
> Default wrecks credit, garnishes future wages, and many other shit things. Forbearance protects against that. It literally only requires proving your situation and notifying them.

**Example 2:**
> Surprisingly it’s worth something. An F500 company hired me straight off of a no name internship since the stuff I did in it was very useful to what they had an opening for

### `hot_take`

**Definition:** A conclusion about the world or the industry with no evidence offered, or with only a story too small to carry it, whether the tone is confident or hedged.

**Example 1:**
> The uncomfortable truth here is Big Tech and F500 companies are filled with unpleasant people that break all these rules OP listed because they simply get things done (whether they are actually good at their job is debatable, what matters is many of them put on a good show for leadership and play the corporate game well).
>
> And guess what, unpleasant people who are in the position of hiring often hire (or even select for) other unpleasant people.
>
> This is all to say, many new grads/early career folks will pretty quickly learn being a normal person is unfortunately not selected for at a lot of tech companies and very few interviewers can even glean that info from a ~1hr interview.

**Example 2:**
> Hear me out. A friend who did math at an ivy league university got a job at the big3 consulting with no internship. It is crazy how much prestige open up the door. So for those losers who said “prestige does not matter” you should put yourself into current fresh grad’s shoes. It is the same for swe which is a prestige whore.

### `vent`

**Definition:** The writer describes their own situation and how it feels, without drawing any conclusion about the world or telling anyone what to do, even if they include numbers.

**Example 1:**
> 150 apps a few oas 0 interviews it’s over for me

**Example 2:**
> lost track atp, i did multiple OAs and got into two interview processes for new grad (i got more interview processes for entry level positions than i did for new grad smh). flunked one of them and the other one i'm not very confident about my chances of passing. i have an offer on the table but not something that i'm content with so i'm still applying and hoping for the best :(

### `advice`

**Definition:** Tells the reader what action to take (try, you should, do X, don't do Y) without evidence for it; a reason that is itself an unsupported claim doesn't count as evidence.

**Example 1:**
> I think the bigger issue is getting past the initial screening. Try referrals and smaller companies too. Your first opportunity doesn’t have to come from a big name company.

**Example 2:**
> You can't control what you did but only what you can do now and in the future. Just focus on making yourself the best candidate with what you can control instead of focusing on what you can't.

### The hardest boundary

**Which two labels:** `backed` and `hot_take`

**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->

Personal experience counts as evidence in this community, but only when it is the writer's own first-hand experience and it directly explains the conclusion. If the story is second-hand ("a friend…") or one story is stretched into a claim about the whole industry, it's `hot_take`, even if it sounds reasonable. So "an F500 company hired me because my internship work matched their opening" is `backed`, and "my friend got into consulting with no internship, so SWE is a prestige whore" is `hot_take`.

Evidence doesn't have to be personal: a specific, checkable fact from any source counts ("BLS projects software jobs to grow 17%, so CS isn't dying" is `backed`), and a specific number counts even without a link. And `backed` needs a conclusion: numbers with no conclusion drawn from them ("referrals got me 4 interviews out of 12, cold apps 0 out of 200, I'm exhausted") are `vent`.

**Other rules I apply in order:**

1. Does evidence directly support a conclusion? → `backed`
2. Is it only about the writer's own situation and feelings, with no conclusion about the world? → `vent`. One general claim ("this industry is broken") makes it not `vent`.
3. Is it mainly telling the reader to do something? → `advice`
4. Otherwise, an unsupported conclusion about the world → `hot_take`, confident or hedged ("maybe it's just me but…" still counts).

Sarcasm is labelled by what it actually means, not its literal words. When a post mixes types (a claim plus some advice), I label it by what most of its words are doing.


---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| `hot_take` | 82 | 39.8% |
| `vent` | 51 | 24.8% |
| `backed` | 37 | 18.0% |
| `advice` | 36 | 17.5% |
| **Total** | 206 | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
> *The post:* "Yeah that sucks. Annoying in this industry that one interviewer can have personal bias or some other issue going on and tank an entire interview process and job opportunity. Had it happen several times."
>
> *Could have been:* `vent` or `backed`
>
> *I chose, because:* In my cold pass I chose `vent`, because the tone is frustrated and it opens with "that sucks". On review it should be `backed`. It makes a general claim about the industry (one interviewer can tank a whole process), so by rule 2 it can't be `vent`. And "had it happen several times" is the writer's own first-hand experience, and it directly explains that claim. I left the cold label unchanged in `labels.csv` so the agreement check measures my real first pass.

**2.**
> *The post:* "renaissance? CS was over-saturated previously due to the hiring spree during scaling phase of big tech. it is just getting back to baseline."
>
> *Could have been:* `vent` or `hot_take`
>
> *I chose, because:* In my cold pass I chose `vent`, because it sounded tired and negative. On review it should be `hot_take`. There is nothing about the writer in it, just a conclusion about the whole industry with no evidence given. This one taught me that tone doesn't decide the label: a gloomy post is only `vent` if it is about the writer's own situation.

**3.**
> *The post:* "Yeah, I could see this. It's just our economy has been a fucking mess for four years now. for there to be a renaissance, The economy has to improve and I'm afraid that it's gonna be a while before that happens.."
>
> *Could have been:* `vent` or `hot_take`
>
> *I chose, because:* In my cold pass I chose `vent`, because of the feeling words ("fucking mess", "I'm afraid"). On review it should be `hot_take`. The feelings are about the economy, not about the writer's own situation, and the main point is an unsupported prediction (CS won't recover until the economy does). By rule 2, one general claim makes it not `vent`.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:* While designing my labels, I proposed adding a fourth label, `advice`, to the three-label plan (`backed` / `hot_take` / `vent`), because unsupported advice was one of the most common things I saw on r/csMajors. I asked the AI to evaluate that choice, and then checked my own understanding of it: I said `advice` responds to the OP's personal case with an action, and `hot_take` is an opinion that doesn't share a story as evidence.
- *What came back:* It agreed `advice` matches how the community talks, but pointed out a conflict: a post like the student-loan comment is advice *and* backed by facts. It suggested checking for support first (supported → `backed`, even if it's advice). It also flagged two problems with my definitions: the model only sees one comment, so "responds to the OP" can't be a feature, and a story isn't automatically evidence (the "my friend got into consulting" post shares a story but is still a `hot_take`).
- *What I changed:* I kept four labels and adopted the support-first rule. I removed "responds to the OP" from `advice` and defined it by the text alone: it tells the reader what action to take, with no reason given. I rewrote `hot_take` to cover a story too small to carry the conclusion. 

**Moment 2**

- *What I asked for:* A stress test. I gave the AI my four definitions and asked for eight r/csMajors-style posts that sit on the boundaries, plus two warm-ups, and labelled them myself before seeing any answers.
- *What came back:* Ten posts. When we compared, four of my labels contradicted my own rules: I called "I got my Amazon offer after 300 LeetCode problems, so grinding works for everyone" `backed`, but it's one story stretched to everyone; I called "referrals got me 4 of 12, cold apps 0 of 200, I'm exhausted" `backed`, but it draws no conclusion; I called a BLS job-growth stat `hot_take` because it wasn't personal experience; and I called "my TA told me…" `backed` even though it's second-hand. Four more showed gaps the rules didn't cover: a hedged claim ("maybe it's just me but…"), a self-report followed by "this industry is broken", advice whose only reason was another unsupported claim, and sarcasm.
- *What I changed:* I rewrote the definitions: evidence is a checkable fact from any source or first-hand experience; `backed` needs a conclusion; one general claim makes a post not `vent`; an unsupported reason doesn't stop advice being `advice`. I also dropped "confident" from `hot_take`. Tone was the distinction I noticed most in Milestone 1, but the test showed it left hedged, unsupported claims with nowhere to go. I added an ordered decision rule, and I label sarcasm by its meaning. The AI drafted the new wording from the rules I agreed to.

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
