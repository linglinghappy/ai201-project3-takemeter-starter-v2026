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

TakeMeter reads comments from r/csMajors, a Reddit community where CS students and new grads talk about jobs, internships and the job market. It sorts each comment into one of four labels. `backed` is a claim with real evidence. `hot_take` is a claim with no real evidence. `vent` is someone talking about their own situation and feelings. `advice` tells the reader what to do, with no evidence. The goal is to help a reader see which comments they can actually trust.

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

**Consistency check dates:** first labelled the 20 `cold` posts on or before 2026-10-20 (when `labels.csv` was first committed) · re-labelled them blind on 2026-10-27, saved as `relabel_check.csv`.

**Where the posts came from:** Public comments from r/csMajors. I copied and pasted them by hand, and I kept each comment whole. The threads cover return offers, interview updates, the new-grad job market, backup majors, AI and coding jobs, and why CS grads like living in NYC. I did not use a scraper.

**How I labelled them:** 

- **20 cold.** I labelled 20 posts first, with only my definitions and no tools. They are marked `cold` in the note column.
- **3 by myself.** I labelled 3 more posts on my own. They are marked `self-labelled`.
- **183 pre-labelled.** An AI tool gave a first label to the other 183 posts, using my four definitions and my decision rules. I read every one and fixed the labels I disagreed with. They are marked `pre-labelled`.
- **Removed 16.** My first file had 222 posts, and `hot_take` was 44%. My balance criterion says no label can be over 40%. So I removed 16 short `hot_take` posts from the NYC thread. They were the most off-topic and repetitive. Now the file has 206 posts.

**Counts per label:**


| Label      | Count | Share |
| ------------ | ------- | ------- |
| `hot_take` | 82    | 39.8% |
| `vent`     | 51    | 24.8% |
| `backed`   | 37    | 18.0% |
| `advice`   | 36    | 17.5% |
| **Total**  | 206   | 100%  |

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

**Base model:** `distilbert-base-uncased`

**Settings:**  3 epochs, learning rate 2e-5, batch size 16, max length 128 tokens, seed 42. I trained on an Apple Silicon GPU (MPS), with torch 2.14.1.

**Anything I changed from the defaults, and why:** Nothing. I kept every default. This is my first run, so I want a clean starting point to compare against next unit.

**Split sizes:** 

Train 144 · Val 31 · Test 31


| Label      | Train | Val | Test |
| ------------ | ------- | ----- | ------ |
| `hot_take` | 58    | 12  | 12   |
| `vent`     | 35    | 8   | 8    |
| `backed`   | 26    | 5   | 6    |
| `advice`   | 25    | 6   | 5    |

`backed` has only 6 posts in the test split, and `advice` has only 5. Both are under 8. One right or wrong answer moves their F1 a lot, so I expect their scores to jump between seeds next unit. `vent` has exactly 8, so it is on the edge.

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

**Pre-labelling disclosure:** I used an AI tool to pre-label 183 of my 206 posts. I gave it my four definitions and my decision rules, and it gave each post a first label. Then I read every post myself and changed the labels I disagreed with. These rows say `pre-labelled` in the note column. I did not use AI for the 20 `cold` posts or the 3 `self-labelled` posts. I also used AI to split pasted Reddit threads into single comments and remove page text like "Upvote" and "Reply". When `hot_take` went over 40%, the AI removed 16 short `hot_take` posts after I asked it to.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->


| Measure          | Baseline | Trained | Difference |
| ------------------ | ---------- | --------- | ------------ |
| Overall accuracy | 0.194    | 0.387   | +0.194     |
| Macro F1         | 0.081    | 0.140   | +0.058     |
| F1 — `advice`   | 0.000    | 0.000   | +0.000     |
| F1 — `backed`   | 0.324    | 0.000   | -0.324     |
| F1 — `hot_take` | 0.000    | 0.558   | +0.558     |
| F1 — `vent`     | 0.000    | 0.000   | +0.000     |

**What I predicted before I looked:**

I predict my trained model will beat the baseline on `hot_take`, because it is my biggest label and the model saw 58 examples of it, but the baseline will do better on `advice`, because "you should…" is easy to spot from the definition alone.

<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**

Both models guess only one label. The baseline labels every post `backed`, and my trained model labels every post `hot_take`. My model's accuracy is 0.194 higher, but only because `hot_take` is my most common label (12 of 31 test posts). Neither model can tell the four labels apart: `advice` and `vent` score 0 on both. So fine-tuning has not taught my model anything yet beyond "guess the biggest label."

I also ran the baseline once with bare label names instead of my definitions. Bare names scored 0.452 accuracy / 0.416 macro F1, much higher than my definitions (0.194 / 0.081). So my definitions made the zero-shot baseline worse. I think this is because my `backed` definition is too broad ("a claim or a piece of advice"), so the model matched every post to it, and the other definitions depend on negations ("without evidence") that NLI models handle badly. My trained model (0.387) also loses to the bare-names baseline, so fine-tuning has not beaten a zero-shot model yet.

<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->

---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->


| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
| ----------- | -------- | --------- | -------- | ----------- | --------- |
| 1. Overall accuracy | ≥ 0.60 in all three seeds | 0.387 | 0.387 | 0.387 | MISSED |
| 2. Per-label F1 | `hot_take`, `vent`, `advice` ≥ 0.50; `backed` ≥ 0.40 | hot_take 0.558, vent 0.000, advice 0.000, backed 0.000 | hot_take 0.558, vent 0.000, advice 0.000, backed 0.000 | hot_take 0.558, vent 0.000, advice 0.000, backed 0.000 | MISSED |
| 3. Balance | every label ≥ 30 posts, none > 40% | smallest 36 (`advice`), largest 39.8% (`hot_take`) | same (dataset-level) | same (dataset-level) | MET |
| 4. Consistency | ≥ 16 of 20 `cold` posts match on re-label | 10 / 20 | same (dataset-level) | same (dataset-level) | MISSED |
| 5. Confidence | most-confident third minus least-confident third ≥ 0.15 | 0.40 − 0.30 = 0.10 | 0.70 − 0.10 = 0.60 | 0.60 − 0.30 = 0.30 | MISSED |

All three seeds ran on an Apple Silicon GPU (MPS) with torch 2.14.1.

Accuracy was 0.387 on all three seeds (spread 0.000), but that is not a sign of stability. On every seed the model predicted `hot_take` for every test post. The split is stratified, so every seed's test split has 12 `hot_take` posts out of 31, and always guessing `hot_take` scores 12 / 31 = 0.387 no matter which posts land in the test set. Training loss only fell from about 1.35 to 1.28 (random guessing over four labels is about 1.39), and with 144 training posts, batch size 16 and 3 epochs the model only took 27 training steps. The model is underfitting: it learned the most common label, not the difference between labels.

Criterion 4 doesn't depend on the seed: it compares my two labellings of the same 20 `cold` posts in `relabel_check.csv`. Criterion 5's numbers don't mean much here. Every prediction is `hot_take`, so each third's accuracy just counts how many real `hot_take` posts it happens to contain.

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

Seed 42. Seeds 7 and 2024 gave exactly the same matrix.

| true \ predicted | backed | hot_take | vent | advice |
|---|---|---|---|---|
| **backed** | 0 | 6 | 0 | 0 |
| **hot_take** | 0 | 12 | 0 | 0 |
| **vent** | 0 | 8 | 0 | 0 |
| **advice** | 0 | 5 | 0 | 0 |

**My biggest off-diagonal number, and what it means:**

The biggest off-diagonal number is 8: all 8 real `vent` posts were called `hot_take`, and 0 real `hot_take` posts went the other way. But this isn't a single boundary the model got wrong. Every column except `hot_take` is 0, so the model calls every post `hot_take` and hasn't learned any boundary yet. That's why I read it as a model problem (too little training), not a labelling problem, even though the notebook says a lopsided direction usually points at labelling.

<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->


| # | Criterion | Target | Verdict | How I decided |
| --- | ----------- | -------- | --------- | --------------- |
| 1 | Overall accuracy | ≥ 0.60 in all three seeds | MISSED | 0.387 on every seed, far below 0.60. |
| 2 | Per-label F1 | `hot_take`, `vent`, `advice` ≥ 0.50; `backed` ≥ 0.40, in all three seeds | MISSED | Only `hot_take` passes (0.558). `vent`, `advice` and `backed` are 0.000 on every seed. |
| 3 | Balance | every label ≥ 30 posts, none > 40% | MET | Smallest label is `advice` with 36 posts; largest is `hot_take` at 39.8%. |
| 4 | Consistency | ≥ 16 of 20 `cold` posts match on blind re-label | MISSED | 10 of 20 matched in `relabel_check.csv`. |
| 5 | Confidence | most-confident third minus least-confident third ≥ 0.15 in all three seeds | MISSED | Gaps were 0.10, 0.60 and 0.30. Seed 42 is below 0.15, so it doesn't hold across all three. |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

**Criterion 1 (accuracy) — a model problem: the model is undertrained and only guesses the biggest label.**
Accuracy is 0.387 on all three seeds, which is exactly 12 / 31, the share of `hot_take` in every stratified test split. The confusion matrix shows why: on every seed, all 31 test posts were predicted `hot_take`. Training loss only went from about 1.35 to 1.28 (random guessing over four labels is about 1.39), and validation accuracy stayed at 0.387 after every epoch. With 144 training posts, batch size 16 and 3 epochs, the model only took 27 training steps. The agreement report is what tells me this is not mainly a labelling problem. My disagreements with staff were on two specific boundaries ("does the fact carry the argument?" and "is it about the writer or the world?"). If messy labels were the main cause, the model would mix up those pairs and still get the other labels right. Instead it predicts `hot_take` for everything, including `backed` and `advice` posts that have nothing to do with those boundaries. The task itself is reachable: the zero-shot baseline with bare label names already scores 0.452.

**Criterion 2 (per-label F1) — mostly the same model problem, plus too few examples for `backed` and `advice`, plus an inconsistent `vent` / `hot_take` boundary.**
`vent`, `advice` and `backed` score 0.000 because the model never predicts them, which is the undertraining from criterion 1. Two other causes will matter once the model does learn. First, `backed` has only 26 training and 6 test posts, and `advice` has 25 and 5, so their F1 will be noisy: one post moves it a lot. Second, my own labels on `vent` vs `hot_take` are inconsistent (see criterion 4): 7 of my 10 re-label changes were on that pair, and the biggest off-diagonal in my matrix is also on that pair (8 `vent` posts called `hot_take`). Right now I can't separate that labelling effect from the undertraining, because the model calls everything `hot_take` anyway.

**Criterion 4 (consistency) — a labelling problem: I applied the `vent` / `hot_take` boundary two different ways.**
Only 10 of 20 posts got the same label the second time. 7 of the 10 changes were between `vent` and `hot_take`: 3 went from `vent` to `hot_take` and 4 from `hot_take` to `vent`. The other 3 involved `advice` (`vent` → `advice`, `hot_take` → `advice`, `advice` → `backed`). So it isn't that I changed my mind about one rule; I'm flipping both ways on the same boundary. My rule says a post that draws any conclusion about the world is not `vent`, but in practice I decided by tone: posts that sounded frustrated became `vent`, and posts that sounded calm became `hot_take`. The agreement report shows the same habit on someone else's rules. I called 4 general claims `reaction` because they sounded personal, even though staff Rule 2 (about the writer vs about the world) covered them, and that rule is the same idea as my `vent` rule. So this is my labelling, not the model, and it is also in my training data: the cold labels in `labels.csv` are the first-pass ones.

**Criterion 5 (confidence) — the same model problem as criterion 1.**
The gap is 0.10 on seed 42, below the 0.15 target. But the model predicts `hot_take` for every post, so the "most confident" and "least confident" thirds only differ in how many real `hot_take` posts they happen to contain. The confidence has no meaning yet because the model hasn't learned to separate the labels. The criterion itself is clear and measurable, so I am not revising it.

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 13 / 30 = 43%

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

> *The post:* "I tracked sleep against session quality for eleven weeks. Under seven hours the next day's intervals were 6-8 seconds per mile slower, every time bar one. Small sample, one runner, but it's consistent enough that I've stopped scheduling hard days after late shifts."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* I think my reading is defensible. The definition asks for a "checkable" fact. This is a private sleep log, and no reader can check it. Staff read "checkable" as "specific and measured". I read it as "someone else could verify it". The rules don't say which one is meant, and every example fact in the taxonomy (a stat, a date, a quote) is public.
>
> *Which pile:* (c)

**2.**

> *The post:* "Everyone blames the hill at 18 miles. I split the field into people who ran the first half under 1:45 and over, and the slowdown after 18 was almost identical for both groups. If the hill were the problem the fast starters would fall apart harder."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right. The writer runs a test on the race results, and the result is the reason for the conclusion. Rule 1 says that is `analysis`. I think I used my own unit 5 idea that a small story can't carry a claim, which is not in the staff rules.
>
> *Which pile:* (a)

**3.**

> *The post:* "Went back through the club results going back to 2012. Every single year the number of people who enter the spring marathon and don't start it sits between 18 and 23 percent. It's not a bad-luck year, it's the base rate."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* Staff is right. Club results are public and checkable, and the 18–23% range is the whole argument. Rule 1 covers this. I applied it loosely.
>
> *Which pile:* (a)

**4.**

> *The post:* "Three of us ran the same session on the same day, different shoes, within 10 seconds of each other over 5 miles. I'm not saying shoes do nothing, but whatever they do was smaller than the noise between three people."
>
> *Staff said / I said:* `analysis` / `hot_take`
>
> *My call, and why:* The rules don't cover this case. The claim is hedged ("I'm not saying shoes do nothing") and the sample is only three people. `hot_take` needs a "confident" claim, and this one is not confident. `analysis` needs a fact that carries the argument, and three runners is very weak. Neither label fits well, and the rules don't say what to do with a careful claim that has weak evidence. Staff also marked this one as hard.
>
> *Which pile:* (b)

**5.**

> *The post:* "Anyone who races more than once a month isn't training, they're just collecting medals."
>
> *Staff said / I said:* `hot_take` / `analysis`
>
> *My call, and why:* Staff is right. This is a claim about a whole group with no support. "Once a month" is part of the claim, not evidence for it. Rule 1 covers this.
>
> *Which pile:* (a)

**6.**

> *The post:* "The club needs to stop pretending the Tuesday session is for everyone. It isn't and it never has been."
>
> *Staff said / I said:* `hot_take` / `reaction`
>
> *My call, and why:* Staff's label is closer, because this is a general claim about the club and not about the writer, so it isn't `reaction` (Rule 2). But the post mostly tells the club what to do ("needs to stop"). The three labels don't say how to handle advice or a call to action. That gap is why I added an `advice` label in my own project.
>
> *Which pile:* (b)

**7.**

> *The post:* "Times are down about 3% since the shoe rules changed, so obviously the shoes are the whole story and the sport has a problem."
>
> *Staff said / I said:* `hot_take` / `analysis`
>
> *My call, and why:* Staff is right. This is almost exactly the Rule 1 example. The 3% is decoration, and "so obviously" does the work, not the number. I treated "has a number" as "has evidence".
>
> *Which pile:* (a)

**8.**

> *The post:* "If you need a gel before 90 minutes you have a fuelling problem, not an energy problem."
>
> *Staff said / I said:* `hot_take` / `analysis`
>
> *My call, and why:* Staff is right. "90 minutes" is part of the claim, not a fact that supports it. Nothing is argued. Rule 1 covers this.
>
> *Which pile:* (a)

**9.**

> *The post:* "Road racing peaked in about 2015 and everything since has been marketing."
>
> *Staff said / I said:* `hot_take` / `reaction`
>
> *My call, and why:* Staff is right. This is a general claim about the whole sport, not about the writer, so Rule 2 makes it `hot_take`. The year is part of the claim, not evidence for it.
>
> *Which pile:* (a)

**10.**

> *The post:* "Track sessions are wasted on anyone running slower than 8 minute miles. You'd get more out of just running more."
>
> *Staff said / I said:* `hot_take` / `analysis`
>
> *My call, and why:* Staff is right. "8 minute miles" is a cut-off inside the claim, not evidence. There are two claims and no support. Rule 1 covers this.
>
> *Which pile:* (a)

**11.**

> *The post:* "Nobody actually enjoys the long run. They enjoy having done it, which is a completely different thing, and the sport would be more honest if it said so."
>
> *Staff said / I said:* `hot_take` / `reaction`
>
> *My call, and why:* Staff is right. It sounds personal and reflective, but "nobody" makes it a claim about everyone. Rule 2 says a general claim is `hot_take`. I followed the tone instead of the rule.
>
> *Which pile:* (a)

**12.**

> *The post:* "Every injury thread on this forum is the same injury and the same three replies."
>
> *Staff said / I said:* `hot_take` / `reaction`
>
> *My call, and why:* Staff is right. It sounds like the writer's own observation, but it is a general claim about every thread, and no count is given. Rule 2 covers this.
>
> *Which pile:* (a)

**13.**

> *The post:* "Got up at 5, drove ninety minutes, and it's cancelled. Standing in the car park in the rain reading the email."
>
> *Staff said / I said:* `reaction` / `analysis`
>
> *My call, and why:* Staff is right. The numbers only describe what happened to the writer. Nothing is argued from them. Rule 3 says a fact has to carry an argument to make a post `analysis`.
>
> *Which pile:* (a)

**14.**

> *The post:* "First run back after eight weeks out. Two miles, slower than my warm-up used to be, and I don't care even slightly."
>
> *Staff said / I said:* `reaction` / `analysis`
>
> *My call, and why:* Staff is right. This is about the writer's own run and feelings. "Eight weeks" and "two miles" describe the run, they don't argue anything. Rule 3 covers this.
>
> *Which pile:* (a)

**15.**

> *The post:* "Watching the last 400 of that and I had to stand up. Still standing up actually."
>
> *Staff said / I said:* `reaction` / `analysis`
>
> *My call, and why:* Staff is right. This is an immediate response to a race happening now, with no argument. "400" is just which part of the race it was. Rule 3 covers this.
>
> *Which pile:* (a)

**16.**

> *The post:* "Blew up at 20 with the pace band still in my hand like it was going to help. Rough one."
>
> *Staff said / I said:* `reaction` / `analysis`
>
> *My call, and why:* Staff is right. This is the writer's own bad race and how it felt. "20" says where it happened, it isn't evidence for a claim. Rule 3 covers this.
>
> *Which pile:* (a)

**17.**

> *The post:* "Third DNF this year. I don't really want to talk about it, just wanted to put it somewhere."
>
> *Staff said / I said:* `reaction` / `hot_take`
>
> *My call, and why:* Staff is right. The writer is reporting their own state, not making a claim about the world, so Rule 2 makes it `reaction`. "Third this year" is a count, but nothing is argued from it.
>
> *Which pile:* (a)

**What the pattern in my disagreements tells me:**

14 of my 17 disagreements are pile (a): the rule covered the post and I applied it loosely. Two are pile (b) and one is pile (c). My mistakes go in two opposite directions on the same question, "does the fact carry the argument?". When a post had any number in it (a time, a distance, a count), I often called it `analysis`, even when the number only described what happened or was part of the claim (8 posts like this). But when a post really did argue from data, I called it `hot_take` (4 posts), probably because I used my own unit 5 rule that a small story can't carry a claim. I also called 4 general claims `reaction` because they sounded personal, even though Rule 2 says a general claim is `hot_take`. This means I don't apply "what counts as evidence" the same way every time. That is a consistency problem, and it probably affects my own 206 labels too, especially the `backed` vs `hot_take` boundary.

---

## The Improvement

**What I changed:** One training setting: `EPOCHS` from 3 to 10. Everything else stayed the same: learning rate 2e-5, batch size 16, max length 128, the same seeds (42, 7, 2024), and the same `labels.csv`. With 144 training posts and batch size 16, this takes training from 27 steps to 90.

**Which diagnosis pointed at it:** Criteria 1, 2 and 5. The before-run predicted `hot_take` for every test post on all three seeds, training loss barely moved (about 1.35 → 1.28, random guessing is about 1.39), and validation accuracy stayed at 0.387 after every epoch. That is undertraining, not labelling: the model wasn't even confusing specific label pairs yet, it just guessed the biggest label. I did not relabel the `vent` / `hot_take` boundary (criterion 4) in this run, because a model that only guesses one label can't show whether relabelling helped.

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
| ----------- | -------- | --------- | -------- | ----------- | --------- |
| 1. Overall accuracy | ≥ 0.60 in all three seeds | 0.613 | 0.613 | 0.742 | MET |
| 2. Per-label F1 | `hot_take`, `vent`, `advice` ≥ 0.50; `backed` ≥ 0.40 | hot_take 0.621, vent **0.462**, advice 0.727, backed 0.667 | hot_take 0.741, vent 0.636, advice **0.333**, backed **0.286** | hot_take 0.774, vent 0.800, advice 0.750, backed 0.500 | MISSED |
| 3. Balance | every label ≥ 30 posts, none > 40% | smallest 36 (`advice`), largest 39.8% (`hot_take`) | same (dataset-level) | same (dataset-level) | MET |
| 4. Consistency | ≥ 16 of 20 `cold` posts match on re-label | 10 / 20 | same (dataset-level) | same (dataset-level) | MISSED |
| 5. Confidence | most-confident third minus least-confident third ≥ 0.15 | 0.70 − 0.50 = 0.20 | 1.00 − 0.30 = 0.70 | 1.00 − 0.60 = 0.40 | MET |

All three seeds ran on an Apple Silicon GPU (MPS) with torch 2.14.1. Bold numbers are the ones below target.

**Confusion matrix — after (seed 42):**

| true \ predicted | backed | hot_take | vent | advice |
|---|---|---|---|---|
| **backed** | 3 | 3 | 0 | 0 |
| **hot_take** | 0 | 9 | 2 | 1 |
| **vent** | 0 | 4 | 3 | 1 |
| **advice** | 0 | 1 | 0 | 4 |

**Did it help, and how do I know:**

Yes. Training for 10 epochs instead of 3 raised accuracy from 0.387 to 0.613–0.742, and I went from 1 to 3 criteria met. But the scores still jump a lot between seeds, and criterion 2 is still missed.

Side by side:

| Measure | Before (3 epochs) | After (10 epochs) |
|---|---|---|
| Overall accuracy (seeds 42 / 7 / 2024) | 0.387 / 0.387 / 0.387 | 0.613 / 0.613 / 0.742 |
| Macro F1 (seeds 42 / 7 / 2024) | 0.140 / 0.140 / 0.140 | 0.619 / 0.499 / 0.706 |
| Criteria met | 1 of 5 (balance) | 3 of 5 (accuracy, balance, confidence) |

Before, the model guessed `hot_take` for every post. Now every label has correct predictions on the diagonal of the matrix, and accuracy beats both the always-`hot_take` score (0.387) and the bare-names zero-shot baseline (0.452) on every seed. Criterion 1 went from MISSED to MET, but only just: two seeds are at 0.613 against a 0.60 target. Criterion 5 went from MISSED to MET, and now it means something, because the model is no longer predicting one label.

Three things are still not good:

- **The result is not stable.** Accuracy moved 0.129 across seeds, more than 10 points, and per-label F1 moved even more (`advice` from 0.333 to 0.750, `backed` from 0.286 to 0.667). The test split has only 31 posts, with 6 `backed` and 5 `advice`, so one post changes those F1 scores by a lot. My dataset is too small for a stable measure.
- **Criterion 2 is still MISSED.** Every label passes on at least one seed but not on all three: `vent` fails on seed 42, and `advice` and `backed` fail on seed 7.
- **The `vent` / `hot_take` boundary now shows up.** The biggest off-diagonal is 4 real `vent` posts called `hot_take`, with 2 going the other way. Now that the model is actually learning, the confusion is on exactly the pair where my own labels were inconsistent: 7 of my 10 re-label changes (criterion 4) were between `vent` and `hot_take`. So my next change would be to relabel that boundary, not more training.

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->

---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->

**Criterion 2 (per-label F1) — still MISSED.**
Every label passes on at least one seed, but not on all three. `vent` fails on seed 42 (0.462). `advice` (0.333) and `backed` (0.286) fail on seed 7.
- *What I'd do:* First, relabel the `vent` / `hot_take` boundary with one clear rule: if a post makes any claim about the world, it is not `vent`, whatever the tone. Then retrain on the same three seeds. After that, add about 30 more `backed` and `advice` posts. They have only 6 and 5 posts in the test split, so one post changes their F1 a lot.
- *Why I stopped:* The milestone allows one change per run. I used it on training length, because that is what my diagnosis pointed at. I ran out of time for a second round.

**Criterion 4 (consistency) — still MISSED (10 / 20).**
Retraining can't fix this. Only my labelling can.
- *What I'd do:* Write a sharper rule for `vent` vs `hot_take`: tone doesn't count, only whether there is a general claim. Relabel every `vent` and `hot_take` row in `labels.csv` with that rule. Then wait at least three days and do the blind re-label again.
- *Why I stopped:* The check needs a three-day gap. I didn't have that time before the deadline.

**Stability.**
After the change, accuracy moved 0.129 across seeds. That is more than 10 points. The test split has only 31 posts, so the scores will keep jumping. The real fix is more data, not more training.

**The gap between what I meant my labels to capture and what the model
learned:**

<!-- Two sentences. Your confusion matrix is the evidence. -->

I meant `vent` vs `hot_take` to be about the writer vs about the world, but the model mixes them up both ways (4 `vent` → `hot_take`, 2 back), on the same pair I flipped 7 times when I re-labelled, so it likely learned tone, not my rule. I meant `backed` to need evidence that carries the claim, but 3 of the 6 `backed` posts were called `hot_take`, so the model doesn't yet notice whether evidence is there.

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
