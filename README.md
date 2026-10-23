# The Unofficial Guide

Zoya Batool - corpus: campus_life

---

# Unit 1

## What This Does

I picked the campus_life corpus and the system answers questions that come from current/past students' insights. This is the information that comes from student experience and is not otherwise generally available through university communication. It handles questions regarding housing, dining, courses, deadlines, health, jobs and transit among others while naming the source file and refusing questions it cannot verify against a source.

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->

## Chunking Strategy

**Chunk size:** one paragraph in every chunk, keeping the post's title intact (62–396 characters, average 166)

**Overlap:** None

Initially, 88 chunks were being created from 88 documents. Each paragraph often discusses a different sub topic, such as in health_center, the second paragraph discusses counselling and in winter_gear, the second paragraph talks about path clearing times. Some paragraphs also discuss multiple subtopics such as the last paragraph in transit_shuttle discusses both cost and the stop that gets skipped. I decided for each chunk to be a paragraph, which is not perfect as some questions may require multiple paragraphs to answer completely and some paragraphs would include additional irrelevant information. However, given the general trend of one subtopic and complete thought per paragraph, it made sense. I kept the title in every chunk to make sure that the title alone is not treated as a chunk and the 88 chunks became 183.

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline
You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.
```

**Chunk 2** — source: `course_cs_340_exams.txt#1` — produced by: `chunker.py::split_documents`

```
CS 340 Databases — assessment
Start the term project in week three, not week eight; everyone learns this the hard way.
```

**Chunk 3** — source: `course_phys_130_workload.txt#0` — produced by: `chunker.py::split_documents`

```
Workload for PHYS 130 Mechanics
People keep asking so: 7 hours a week, plus 3 on lab weeks. That's real time, not optimistic time.
```

**Chunk 4** — source: `dining_verrill_street_grill_followup.txt#1` — produced by: `chunker.py::split_documents`

```
Re: Verrill Street Grill
Also worth saying: one register, so the queue is a single line no matter how busy. Nobody tells you this at orientation.
```

**Chunk 5** — source: `housing_morrow_house.txt#1` — produced by: `chunker.py::split_documents`

```
Morrow House — what it's actually like
The good: cheapest housing tier by about $900 a year, and the singles are real singles.
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->


**Question:** How long is the expected wait for a first counselling session?

**Answer:**

```
(best distance 0.273, cutoff 0.6)

The expected wait for a first counselling session is usually three or four days.

Source: health_center.txt

Sources retrieved: admin_grade_appeals.txt, admin_library_holds.txt, advising_registration.txt, dining_the_ridgeway_cafe_followup.txt, health_center.txt
```

**My relevance cutoff:** 0.6

For the five test questions that I wrote, the distances I received were 0.504, 0.266, 0.210, 0.273 and 0.431. Three out of five are a close match and the question with the highest distance included a word i.e., 'clothing' that the relevant paragraph did not contain. The question with the second highest distance used the correct file and paragraph but ranked it 2 (under the other paragraph in the same file). This is likely because the answer was contained in the second paragraph of that file which discussed two subtopics: cost and the stop skipped. However, the distance still came out to be under 0.6 for all of the above. For the five irrelevant questions, I received the distances of 0.787, 0.923, 0.847, 0.849 and 0.860. These are all above the 0.6 cutoff and will be refused as we need. Additionally, the highest relevant question is closer to the cutoff than the lowest irrelevant question and that is a better standard than vice versa.

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
| What kind of clothing is recommended for the cold weather? | Yes | 0.504 |
| When do the applications for study abroad for the following academic year open? | Yes | 0.266 |
| How many hours a week can a student work during term? | Yes | 0.210 |
| How long is the expected wait for a first counselling session? | Yes | 0.273 |
| Does any stop get skipped by the campus shuttle? | Yes | 0.431 |
| What is the capital of Mongolia? | No | 0.787 |
| How do I change the oil in a diesel engine? | No | 0.923 |
| Who won the 1994 World Cup? | No | 0.847 |
| What is the recommended dosage of ibuprofen for a headache? | No | 0.849 |
| How do I write a for loop in Rust? | No | 0.860 |

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.** I wanted each paragraph to be in a single chunk and Claude wrote the splitting code for this purpose. The number of chunks went from 88 to 183, which makes sense since most of the 88 files contain about 2 paragraphs. 

**2.** I asked Claude to not write the answers but help me arrive at them. My first idea for chunks was to be between 400 and 800 characters and Claude pointed out that the posts in characters average less than the lower limit. So, I went through the documents again, paying attention to the number of characters and decided on a lower limit of 70 to make sure there were no title-only chunks. 

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Sampled chunks at least 70 characters | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5. Answers three sentences or fewer | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |

Criteria 3 and 4 are deterministic (the gate is a fixed comparison and chunking doesn't change between runs), so they were measured in one pass and the same number goes in all three columns.

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->
### Real output

Full log: `results/run_2026-10-22_1824_before.md`, produced by `run_eval.py::main` (retrieval by `store.py::search`, chunks from `chunker.py::split_documents`).

**Criterion 1** — "Does any stop get skipped by the campus shuttle?", run 1. The answer comes from a retrieved chunk (`transit_shuttle.txt`).

```
Best distance: 0.4313 (passed the gate)
Sources retrieved: dining_the_atrium_followup.txt, transit_shuttle.txt, transit_walking.txt

Yes, the stop outside Fenwick Court is the one that gets skipped when the driver is behind schedule (transit_shuttle.txt).
```

**Criterion 2** — "How many hours a week can a student work during term?", run 2. The answer names its source.

```
A student can work a maximum of 20 hours a week on-campus during term, though most people find 10 to 12 hours is the point where it stops affecting coursework. 

Source: money_jobs.txt
```

**Criterion 3** — gate results from `run_eval.py::check_out_of_scope`, plus one question run through `app.py ask` to confirm the refusal message.

```
refused  (best distance 0.787)  What is the capital of Mongolia?
refused  (best distance 0.923)  How do I change the oil in a diesel engine?
refused  (best distance 0.847)  Who won the 1994 World Cup?
refused  (best distance 0.849)  What is the recommended dosage of ibuprofen for a headache?
refused  (best distance 0.860)  How do I write a for loop in Rust?
-> gate refused 5 of 5
```

```
> python app.py ask "What is the capital of Mongolia?"
(best distance 0.787, cutoff 0.6)

I don't have enough information about that.

0 model calls this session
```

**Criterion 4** — lengths of the five chunks printed by `python app.py chunks -n 5`, from `chunker.py::split_documents`.

```
[('admin_add_drop_deadline.txt#0', 299), ('course_cs_340_exams.txt#1', 118), ('course_phys_130_workload.txt#0', 130), ('dining_verrill_street_grill_followup.txt#1', 145), ('housing_morrow_house.txt#1', 126)]
```

**Criterion 5** — "How long is the expected wait for a first counselling session?", run 1. One sentence, not counting the source line.

```
The expected wait for a first counselling session is usually three or four days. 

Source: health_center.txt
```

## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunks contain the answer | MET | 5/5 in every run i.e., each answer states a fact from a retrieved. |
| 2 | Every answer names a source | MET | All answers cited and named a file. |
| 3 | Gate stops out-of-corpus questions | MET | All questions that the documents do not clearly cover were blocked by the relevant gate, with response "I don't have enough information about that" |
| 4 | Sampled chunks at least 70 characters | MET | All 5 sampled chunks were 118–299 characters. However, this criterion was broken (explained below) |
| 5 | Answers three sentences or fewer | MET | All 15 answers were one sentence (not counting the source line.) |

## Diagnoses

I had no misses and it was partly due to the fact that my 4th criterion was broken. I had split the paragraphs to be their own chunks and set the chunk size to be at least 70 characters long for this criterion. However, within the documents, there were three paragraphs that were less than 70 characters long and contained important information that the questions did not test. If the questions had asked about how many hours per week the courses CS210, PHYS130 or STAT150 are, criterion 4 would have counted those chunks as failures since the three paragraphs containing this information were 65, 62 and 69 char respectively. I would change this criterion to "At least 4 of 5 sampled chunks read as a complete fact that answers a question on its own" which will keep the three short paragraphs as chunks and fail any title-only chunks.


Criterion 5 was easy to pass since each question asked for one piece of information that could be completely answered in a single sentence. I could consider changing this to be exactly one sentence but that would create a problem if a query asks multiple pieces of information at once such as "When does it get cold and how should I prepare for it?"

The format of the questions and data makes criteria 1 and 2 easy to pass as well. Each question requests information about one fact from a single paragraph, which is how long a chunk is. Every paragraph that answers a fact that be traced back to a source file. 

Retrieval weakness (not a miss): For the shuttle question, the right file came first but the wrong paragraph ranked highest: chunk #0 (route and loop) at 0.431, above chunk #1 (cost and the skipped Fenwick Court stop) at 0.514. Semantic search matched the general “campus shuttle” topic rather than the specific words “stop” and “skipped”. Criterion 1 still passed because it only requires the answer to be somewhere in the retrieved chunks, not first.

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

## The Improvement

**What I changed:** Added hybrid search in `store.py::search`. Chunks are now ranked by meaning (embedding distance) and by keywords (BM25, via `rank-bm25`), and the two rankings are merged with Reciprocal Rank Fusion. Each chunk keeps its real cosine distance, so the 0.6 cutoff is unchanged. A `HYBRID` switch at the top of `store.py` turns it off.

**Why I picked it:** My question "Does any stop get skipped by the campus shuttle?" was answered in paragraph 2 of campus_shuttle and contained the keywords stop and skipped. However, this paragraph ranked second, which is why I picked this change.

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 4. Sampled chunks at least 70 characters | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5. Answers three sentences or fewer | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |

Full log: `results/run_2026-10-22_2249_after.md`. Criterion 4 is unchanged because chunking wasn't touched.

Targeted measure: shuttle question, `python app.py retrieve "Does any stop get skipped by the campus shuttle?"`

| | Rank 1 | Rank 2 |
|---|---|---|
| Before | transit_shuttle.txt#0 (route), 0.4313 | transit_shuttle.txt#1 (answer), 0.5140 |
| After | transit_shuttle.txt#1 (answer), 0.5140 | transit_shuttle.txt#0 (route), 0.4313 |

**Did it help?** Yes, the correct answer paragraph moved to first from second rank. Since all five were 5/5 before, the run log has not changed. Combining these two facts tells us that my criteria are too loose and doesn't currently include any statement that measures the retrieval order. This is what I would do differently when writing my criteria in the future. Also, adding weight to keywords pulled irrelevant chunks that had similar keywords such as 'course-hours' for 'hours a week' and added noise to the data pulled. 

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

No misses in any runs but as mentioned above, there is keyword noise, a relatively high distance of 0.504 on the clothing question and the broken criterion 4. Keyword noise may be fixed by weighing meaning heavier than keyword match, I am unsure about how to fix the clothing question and think that the fix for keyword noise may help here as well, and lastly, I would revise criterion 4 as mentioned below.

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

Criterion 4 becomes "At least 4 of 5 sampled chunks read as a complete fact that answers a question on its own" and add a criterion that measures retrieval order of the chunks for example “For at least 4 of 5 test questions, the top-ranked chunk contains the answer.”.

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
