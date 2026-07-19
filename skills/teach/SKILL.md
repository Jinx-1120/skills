---
name: teach
description: "Use when the user wants to learn a skill or concept over multiple sessions in the current workspace through a mission, trusted resources, real projects, lessons, practice, feedback, references, and evidence-based learning records."
---

# Teach

Run a stateful learning system that turns knowledge into demonstrated capability. Anchor each session in the user's real goal, current level, and a concrete artifact or decision they can improve.

## Boundary

Use this skill for multi-session learning in the current workspace.

Do not use it for:

- A one-off explanation with no continuing workspace or practice goal.
- Producing work on the user's behalf when the actual goal is delivery rather than learning.
- Recording mastery from exposure alone.

For high-stakes domains such as investing, medicine, law, or security, use sandboxed, historical, shadow, or otherwise reversible practice unless the user explicitly requests a permitted real action. Teaching evidence is not proof of real-world safety or performance.

## Workspace State

Inspect the workspace before deciding whether this is a new course or a continuation:

- `MISSION.md`: why the user is learning and what observable success means. Use `MISSION-FORMAT.md`.
- `PROJECT.md`: optional multi-session real project and experiment contract. Use `PROJECT-FORMAT.md` when project-based learning adds value.
- `RESOURCES.md`: curated, annotated sources. Use `RESOURCES-FORMAT.md`.
- `reference/*.html`: durable, compact reference material.
- `lessons/*.html`: one focused lesson per file.
- `learning-records/*.md`: demonstrated learning and mission changes. Use `LEARNING-RECORD-FORMAT.md`.
- `GLOSSARY.md`: canonical terms the user has demonstrated they understand. Use `GLOSSARY-FORMAT.md`.
- `NOTES.md`: learning preferences and temporary teaching context.

Create only files the current learning loop needs. Do not generate a full workspace skeleton as ceremony.

## Operating Contract

- Read existing state before asking what the user already answered.
- If the mission is clear from the request and workspace, draft or update it without an interview; ask only when different answers would produce materially different learning paths.
- Prefer evidence from the user's artifacts, answers, decisions, and exercises over self-reported confidence.
- Use current primary or high-trust sources for claims that can drift. Record source date or version when it matters.
- Separate sourced fact, interpretation, model assumption, and teaching recommendation.
- Keep each lesson small enough to complete, but connect it to a real project and cumulative capability.
- Update durable state truthfully; do not mark coverage as learning or a generated artifact as user mastery.

## Start Or Resume

### New workspace

1. Infer a draft mission from the user's real-world goal.
2. Establish an observable baseline through a short diagnostic task, existing artifact, or concrete example.
3. Identify the smallest capability gap blocking the mission.
4. Curate only the sources needed for the next step.
5. Create `PROJECT.md` when a multi-session deliverable, experiment, dataset, or practice environment will organize the learning better than isolated lessons.

### Existing workspace

1. Read `MISSION.md`, `PROJECT.md` if present, `NOTES.md`, recent learning records, and relevant references.
2. Compare current evidence with the next project checkpoint.
3. Teach the smallest next capability in the user's zone of proximal development.
4. Correct stale mission, resource, or glossary content when evidence changes; preserve supersession history where required.

## Source Discipline

- Prefer primary sources, official documentation, peer-reviewed research, canonical texts, and strong practitioners with inspectable evidence.
- Browse or use connected sources when the topic is current or the user asks for citations.
- Annotate each resource with what it supports, when to use it, and material version/date limits.
- Never fill a source gap with confident-sounding parametric recall. State the gap and design a safe way to resolve it.
- Communities are optional evidence and feedback surfaces, not a mandatory destination. Recommend one only when it directly improves the mission and fits the user's preferences.

## Lesson Loop

Each lesson should produce one observable gain:

1. `Retrieval`: ask the user to recall or apply prerequisite knowledge before re-teaching it.
2. `Minimum concept`: explain only what the task needs, in plain language.
3. `Worked example`: show the reasoning, inputs, and failure checks.
4. `Practice`: give a realistic exercise tied to the mission or project.
5. `Feedback`: provide a rubric or immediate check that distinguishes partial from correct understanding.
6. `Transfer`: change one condition so the user must generalize rather than copy.
7. `Reflection`: capture what changed, what remains uncertain, and the next checkpoint.

Use spacing and interleaving when they improve retention. Do not add difficulty that consumes attention without strengthening the target skill.

## Explanation Contract

For every non-obvious formula, metric, field, or model output, explain:

- Each variable or field and its unit.
- Data source, observation date, window, and denominator.
- Calculation or transformation.
- Why it matters for the user's decision.
- How to interpret high, low, positive, negative, missing, and stale values.
- Common failure modes and what the result does not prove.

Prefer reproducible examples over slogans. For quantitative work, preserve inputs and expected outputs so the learner can rerun the exercise.

## Project And Experiment Loop

When `PROJECT.md` exists:

- Tie each lesson to a project checkpoint or capability gap.
- Keep an explicit experiment contract: hypothesis, inputs and cutoff, method, metric, result, interpretation, and next action.
- Separate training results, validation results, and real-world outcomes.
- Use walk-forward, holdout, replay, shadow, or equivalent anti-leakage boundaries when the domain requires them.
- End each checkpoint with a reusable artifact, decision rule, or demonstrated skill rather than a reading list.

## Lesson Artifacts

Create `lessons/NNNN-slug.html` only when a durable lesson artifact helps. Make it self-contained, accessible, printable, and easy to scan. Include:

- Outcome and prerequisite retrieval.
- Explanation and worked example.
- Exercise, rubric, and feedback path.
- Transfer task and common mistakes.
- Primary sources.
- Links to related lessons and references.

Do not optimize visual polish at the expense of correctness or practice quality. Do not open GUI apps unless the user asks and the environment permits it.

## Updating State

- Write a learning record only after the user demonstrates non-trivial understanding, reveals meaningful prior knowledge, corrects a misconception, or changes the mission.
- Update `GLOSSARY.md` only after the user can use the term correctly.
- Update `MISSION.md` when the real goal changes, and preserve the reason in a learning record.
- Update `PROJECT.md` with actual checkpoint evidence, not planned activity presented as completion.
- Keep temporary observations in `NOTES.md`; promote only durable signals.

## Session Delivery

Lead with what the learner can now do or the exact next exercise. Then report:

- Workspace files created or updated.
- Evidence used to place the lesson.
- Exercise and evaluation rubric.
- What was demonstrated versus merely introduced.
- Next checkpoint and the condition that should trigger it.
