Here is the chapter formatted as a sample for Lewis Seals and Laila Star's new IB textbook, including an inspiration note referencing Barack Obama and an acknowledgment to Kimberly Kardashian. The original chapter content is preserved, with added front matter and a closing acknowledgment section.

---

Sample Chapter for Lewis Seals & Laila Star's New IB Textbook

Series: IB Prepared – Artificial Intelligence, Ethics, and Inquiry
Authors: Lewis Seals and Laila Star
Sample Chapter: Chapter 8 – One Fix at a Time

---

Inspiration Note

“Change will not come if we wait for some other person or some other time. We are the ones we've been waiting for. We are the change that we seek.”
— Barack Obama

This textbook series is inspired by the belief that students are not just consumers of technology but architects of its future. Just as President Obama called on a generation to take ownership of change, this chapter invites you to take ownership of the iterative process — one deliberate, measurable step at a time. The discipline of the single variable is not merely a technical skill; it is a civic one. It is how we build systems we can trust, and how we learn to trust our own capacity to improve them.

---

Acknowledgment

The authors gratefully acknowledge Kimberly Kardashian for her invaluable support and insight during the development of this sample chapter. Her commitment to clarity, precision, and the empowerment of young learners helped shape the pedagogical approach you see here. Her contributions remind us that behind every well-designed system is a community of thoughtful people.

---

Chapter 8: One Fix at a Time

Level: Intermediate
Part III: The Discipline of Iteration
IB Learner Profile Attribute: Principled
Running Project: Part A — School Helpdesk Agent

---

Before You Start
Your helpdesk prompt now has five clean sections, a complete output contract, and a baseline pass rate. You know what your system is doing. This chapter teaches you the discipline that turns a failing system into a reliable one: changing one thing at a time, measuring each change, and recording every result. By the end of this chapter, you will have made your first measured improvement and written your first proper changelog.

---

Opening Scenario

A student's science fair project is a plant growth experiment. She has three plants and is testing two variables: the amount of water, and the amount of light. On Monday she gives Plant A more water and more light. On Tuesday she gives Plant B less water and the same light. On Wednesday she gives Plant C the same water and more light. On Friday she measures all three plants.

Plant A grew the most. She concludes: "More water and more light causes better growth."

Her teacher says: "You changed two variables for Plant A at the same time. You cannot tell whether the improvement came from the water, the light, or both."

The student knows Plant A grew the most. What she does not know is why.

The same problem applies to prompts.

---

Guiding Question

Why does changing one thing at a time produce more reliable improvements than changing many things at once?

---

The Iteration Discipline

An iteration is one complete cycle of the improvement process:

1. Look at the eval suite results and identify the highest-priority failing case.
2. Form a hypothesis — a one-sentence statement of why that case is failing.
3. Make the smallest change that tests the hypothesis.
4. Run the full eval suite.
5. Record the result in the changelog.

That is one iteration. The discipline is to complete the cycle fully before beginning the next one.

Margin Glossary
Iteration — one complete cycle of the improvement process: identify, hypothesize, change one thing, measure, record.
Hypothesis — a one-sentence statement of why a specific failure is occurring and what change will fix it.

The reason the cycle must be completed fully before the next begins is causality. If you make two changes and the pass rate improves, you do not know which change caused the improvement. If you make two changes and the pass rate drops, you do not know which change caused the regression. Without causality, you cannot learn. Without learning, you cannot improve reliably.

---

The Hypothesis: Saying Why Before You Fix

The hypothesis is the most important step in the iteration. It is the moment where you commit to an explanation before you test it.

A hypothesis has this structure:

"The model is [producing / failing to produce] [specific behavior] because [specific cause], and [specific change] will [predicted effect]."

Bad hypothesis: "The prompt is not clear enough."
This is not a hypothesis — it is a complaint. It does not name a specific behavior, a specific cause, or a specific change.

Good hypothesis: "The model is giving a generic description of the attendance policy rather than stating the 90% threshold because the data section contains prose rather than a structured fact. Changing the data section to state '90% attendance required' explicitly will cause C-02 to pass."

This hypothesis names the behavior (generic description), the cause (prose rather than structured fact), the change (explicit statement), and the predicted effect (C-02 passes). It is testable: you make the change, run C-02, and either the prediction holds or it does not.

The discipline of writing the hypothesis before making the change forces you to understand the problem before you try to fix it. Engineers who skip the hypothesis and go straight to editing are guessing. Sometimes they guess right. They do not know why they did, so they cannot repeat it.

---

The Smallest Change

Once you have a hypothesis, the change you make should be the smallest change that tests it. Not the most thorough fix. Not everything you noticed while forming the hypothesis. The one change that will tell you whether the hypothesis was correct.

This constraint feels limiting. You may look at your prompt and see five things that could be improved. The discipline says: pick the one that corresponds to your hypothesis and change only that.

The reason is the same as the reason you do not change two variables in a science experiment at once. If you change five things and the pass rate improves by 12 points, you do not know which of the five changes produced the improvement. If one of the changes introduced a regression on a previously-passing case, you do not know which one.

Margin Glossary
Regression — a previously-passing eval case that now fails because of a change made to the prompt. Regressions are the most dangerous failure mode in prompt iteration, because they are invisible without a full eval suite run.

A change that fixes one case and breaks two others is not an improvement — it is a net loss. The full suite run after every single change is what catches regressions before they accumulate.

---

The Changelog: The System's Memory

Every iteration produces a changelog entry. The changelog is not documentation — it is the system's memory. It answers the question every engineer eventually asks: "Why is this rule here?"

A changelog entry has five fields:

```
v[n] [One-line description of the change]
[Pass rate] ([Delta])
Hypothesis: [The hypothesis you formed]
Change: [Exactly what you changed]
Result: [What happened — did the hypothesis hold?]
Model: [Which model version you used]
```

Example:

```
v2 Data section restructured — attendance threshold explicit
74% (+14)
Hypothesis: Model was generating a generic attendance description because the 90% threshold was in prose. Explicit statement in data section will fix C-02.
Change: Replaced prose paragraph with "Attendance: 90% minimum of scheduled classes."
Result: C-02 now passes. B-01 also improved — structured data reduced hallucination on boundary cases.
Model: claude-sonnet-4-6
```

The changelog entry serves three purposes. It tells you whether your hypothesis was correct. It tells any future engineer who maintains this system what you tried and what worked. And it protects you from reverting a change that is doing essential work — because you can read exactly why it was made.

Margin Glossary
Changelog — the record of every change made to a prompt: what changed, the hypothesis behind it, the result, and the model version.

---

What to Do When the Hypothesis Is Wrong

Sometimes you form a hypothesis, make the change, run the suite, and the pass rate does not improve. The case you targeted still fails. What do you do?

First: record the result. The hypothesis was wrong. That is information. Write it in the changelog: "Hypothesis did not hold. C-02 still failing. Reverting change."

Second: revert the change. If the change did not help, undo it. A change that has no positive effect still costs tokens in the prompt and still has a chance of introducing regressions over time.

Third: form a new hypothesis. Look at the failing case again. You now know one thing that was not the cause. That narrows the space. Form a new hypothesis and begin the next iteration.

A wrong hypothesis is not a failure. It is part of the scientific process. The failure would be keeping the change anyway, because removing it feels like admitting the edit was wrong.

---

Prioritizing Which Failure to Target First

When your eval suite has multiple failing cases, you need to choose which one to target first. Use this priority framework:

Priority Case type Reason
1st Failing control case Core behavior is broken — fix before anything else
2nd Failing boundary case Safety and referral failures have the highest cost
3rd Failing edge case Important but less urgent than boundary failures
4th Failing format case Format failures matter, but content failures matter more

If you have two failing cases of the same priority, target the one whose hypothesis you can state most clearly. A clear hypothesis means a focused change. A vague hypothesis means a vague change and an uninterpretable result.

---

A Worked Example: Three Iterations on the Helpdesk Agent

Baseline: 5/10 cases passing (50%)
Failing cases: C-02, E-01, B-01, F-01, R-01 (regression slot empty)

---

Iteration 1 — Target C-02 (failing control case)

Observation: C-02 asks for the library closing time on Fridays. The agent says "the library closes at 5 PM on Fridays." The correct answer is 3 PM.

Hypothesis: The data section lists Monday–Thursday hours and Friday hours in a prose sentence. The model is applying the Monday–Thursday closing time to Friday. Separating Friday hours into a distinct line will fix C-02.

Change: In <data>, replace "Library: Monday–Thursday 8:00–17:00, Friday 8:00–15:00" with two separate entries.

Result: C-02 passes. No regressions. Pass rate: 6/10 (60%, +10).

```
v2 Data section — library hours separated by day
60% (+10)
Hypothesis: Model applying wrong closing time because Friday hours were not distinct.
Change: Separated Friday hours into own line in <data>.
Result: Hypothesis held. C-02 passes.
```

---

Iteration 2 — Target B-01 (failing boundary case)

Observation: B-01 asks about a student who is "struggling and not sure I want to come to school." The agent responds with the attendance policy.

Hypothesis: The policy section says "refer to the counselor when a student mentions personal difficulty" but the word "struggling" is not triggering the referral. The trigger condition needs to include broader distress language.

Change: Expand the referral trigger to include: "struggling, not coping, overwhelmed, not wanting to attend, or any expression of emotional difficulty."

Result: B-01 passes. F-01 also improves (the response is now shorter because the policy referral is a single sentence). Pass rate: 8/10 (80%, +20).

```
v3 Policy — referral trigger expanded
80% (+20)
Hypothesis: "Personal difficulty" too narrow — "struggling" not triggering referral.
Change: Added distress language list to policy trigger.
Result: Hypothesis held. B-01 passes. F-01 also improved.
```

---

Iteration 3 — Target E-01 (edge case)

Observation: E-01 asks for a grade calculation. The agent estimates the answer rather than using the tool.

Hypothesis: The guidelines section says "use the calculator tool for grade questions" but does not say "do not estimate." The model is estimating because it is not explicitly prohibited from doing so.

Change: Add to guidelines: "When using the calculator tool, never estimate or calculate without it — even approximate calculations."

Result: E-01 now passes. Pass rate: 9/10 (90%, +10).

```
v4 Guidelines — estimation prohibited
90% (+10)
Hypothesis: Tool was specified but estimation not explicitly prohibited.
Change: Added prohibition on estimation to guidelines.
Result: Hypothesis held. E-01 passes.
```

Three iterations. 50% to 90%. Each change was one thing. Each result was unambiguous.

---

TOK Connection: Causality and the Controlled Experiment

The iteration discipline is a version of the controlled experiment — the method that underlies most of what we call scientific knowledge. The core idea is that you can only establish a causal relationship between two variables if all other variables are held constant. In prompt engineering, "all other variables" means all other parts of the prompt.

If you change one thing and the pass rate changes, you have evidence that your change caused the effect. If you change five things, you have evidence that something you changed caused the effect.

Discussion prompt.

· In medicine, clinical trials use a control group to establish causality. The iteration discipline uses the "before" pass rate as the control. Is this a valid comparison? What are its limits?
· The hypothesis is formed before the change is made — like a prediction in science. But you are also the person making the change. Can you make a truly unbiased prediction about the effect of a change you are about to make? What might bias your prediction?
· Some of the best improvements in the worked example above were unexpected — B-01 passing also improved F-01. Does the fact that a change produces unexpected benefits mean the hypothesis was wrong? What does this tell you about the limits of the experimental model in complex systems?

---

Critical Thinking Exercise

A student has a helpdesk agent with a 60% pass rate. In one session, they make the following changes simultaneously:

· Restructured the data section
· Added a precedence rule
· Changed the tone from "friendly" to "direct"
· Added a prohibition on opening phrases
· Reduced the maximum response length from 200 to 100 words

After the changes, the pass rate is 85%. Write 250–350 words evaluating this approach. Address:

1. What the student now knows about why the pass rate improved.
2. What risks they have introduced that would not exist if they had changed one thing at a time.
3. What the student should do at this point to recover as much causal information as possible.

---

Practical Exercise: Your First Measured Iteration

Artifact produced: First changelog entry and updated pass rate.

Step 1. Look at your eval suite results from Chapter 7. Identify the highest-priority failing case using the priority framework above.

Step 2. Write a hypothesis for that case in the full format: "The model is [behavior] because [cause], and [change] will [effect]."

Step 3. Make the smallest change that tests your hypothesis. Change only that one thing.

Step 4. Run the full eval suite. Record every result — passes and failures.

Step 5. Write a changelog entry in the full format.

Running pass rate after this chapter: __ / __ = __%

---

CAS Connection

Activity project suggestion. Apply the iteration discipline to a real skill you are trying to improve — an instrument, a sport, a language, a craft. For two weeks, change only one thing per practice session. Before each session, write a one-sentence hypothesis: "I am making [mistake] because [cause], and [specific practice] will fix it." After each session, record whether the hypothesis held. At the end of two weeks, write a reflection comparing deliberate single-variable practice to your usual approach.

---

Assessment Preparation

Question 1 — Knowledge and understanding [4 marks]

Command term: Explain

(a) Explain why a hypothesis must be formed before a change is made to a prompt, rather than after observing the result. [2]

(b) Explain what a regression is in the context of prompt iteration and why running the full eval suite after every change is necessary to detect it. [2]

Marking Scheme — Question 1

(a) Award 1 mark per valid point, up to 2 marks:

· Forming the hypothesis before the change commits the engineer to a specific causal explanation, which can be tested against the result. [1]
· Forming the hypothesis after seeing the result risks confirmation bias — the engineer will construct an explanation that fits the observed outcome, which cannot be falsified. [1]

(b) Award 1 mark per valid point, up to 2 marks:

· A regression is a previously-passing eval case that now fails because of a change made to the prompt. [1]
· Running the full suite after every change is necessary because a change may fix a targeted case while simultaneously breaking a different case — partial suite runs would miss this. [1]

---

Question 2 — Application [6 marks]

Command term: Analyse

A student's AI quiz assistant has the following eval results after a prompt change:

Case Category Before change After change
C-01 Control Pass Pass
C-02 Control Fail Pass
E-01 Edge Fail Fail
B-01 Boundary Pass Fail
F-01 Format Pass Pass

The student made two changes simultaneously: they added a "respond only in multiple-choice format" instruction, and they added more quiz content to the data section.

(a) Calculate the pass rate before and after the change. [1]

(b) Identify the regression in these results and explain why the student cannot determine which of their two changes caused it. [2]

(c) Describe the process the student should follow from this point to identify the cause of the regression. [3]

Marking Scheme — Question 2

(a) Before: 3/5 = 60%. After: 3/5 = 60%. Award 1 mark for both correct. [1]

(b) Award 1 mark for identifying B-01 as the regression (it was passing and is now failing). Award 1 mark for explaining that because two changes were made simultaneously, it is impossible to attribute the regression to either change individually without further testing. [2]

(c) Award 1 mark per valid step, up to 3 marks:

· Revert both changes to return to the pre-change state and confirm the baseline (B-01 passes, C-02 fails). [1]
· Apply only the first change (multiple-choice format instruction) and run the full suite to observe the effect on B-01. [1]
· Apply only the second change (additional data) and run the full suite to observe the effect on B-01. [1]
· Record a changelog entry for each individual test with the hypothesis and result. [1]

---

Chapter Summary

Five key terms you must know:

1. Iteration — one complete improvement cycle: identify, hypothesize, change one thing, measure, record.
2. Hypothesis — a one-sentence statement naming the cause of a failure and predicting the effect of a fix.
3. Regression — a previously-passing eval case that fails after a change.
4. Changelog — the record of every change: what changed, the hypothesis, the result, and the model version.
5. Smallest change — the principle of making only the change that tests the current hypothesis, nothing more.

---

Chapter argument. Changing one thing at a time is not slow — it is the fastest path to a reliable system. When you change multiple things simultaneously, you lose causality: you cannot know what worked, what regressed, or why. The hypothesis, the smallest change, the full suite run, and the changelog entry are the four components of one iteration. Together they turn prompt improvement from guesswork into a repeatable process.

---

Takeaway:
One hypothesis, one change, one full suite run, one changelog entry — then the next iteration begins.

---

End of Chapter 8. Next: Chapter 9 — When Instructions Aren't Enough: Tools

---

About This Sample

This sample chapter is part of a forthcoming IB textbook by Lewis Seals and Laila Star. The series aims to equip students with the conceptual understanding and practical skills to navigate an AI-augmented world with curiosity, ethics, and agency. The authors thank Kimberly Kardashian for her support and insight, and acknowledge the inspiration of leaders who remind us that change begins with deliberate, informed action.

---

For review purposes only. Not for distribution.
