# Pipeline Configuration

Fill this in and attach it alongside MASTER_PROMPT.md when starting the pipeline.

---

## 1. YOUR IDEA

Paste your raw idea below. Be as messy or polished as you like — the pipeline handles both.

```
[PASTE YOUR IDEA HERE]
```

---

## 2. ITERATION COUNT

How many debate iterations to run. Each iteration covers a different dimension of your idea.

- **Recommended:** 6-10 for a full business idea, 3-5 for a feature or small concept.
- **Minimum:** 3 (below this, coverage is too thin).
- **Maximum:** 15 (beyond this, diminishing returns and repetition).

```
ITERATIONS: ___
```

---

## 3. RANDOMNESS / DIVERSITY STRATEGY

How should the pipeline introduce variation across iterations? Pick ONE primary strategy:

### Option A: Dimension Rotation (Recommended)
Each iteration attacks a different aspect of the idea. The pipeline auto-selects dimensions based on your idea (e.g., technical feasibility, revenue, UX, competition, operations, legal, scalability).

```
DIVERSITY_STRATEGY: dimension_rotation
```

### Option B: Perspective Shift
Each iteration, the Adversary adopts a different stakeholder lens (e.g., investor, end user, regulator, competitor, engineer, shop owner). Same dimension can repeat, but from a different angle.

```
DIVERSITY_STRATEGY: perspective_shift
```

### Option C: Escalating Rigor
Early iterations are friendly and constructive. Later iterations become increasingly adversarial — the final iteration is a full "kill the idea" attempt.

```
DIVERSITY_STRATEGY: escalating_rigor
```

### Option D: Combined (Advanced)
Combines dimension rotation with escalating rigor. Most thorough but longest.

```
DIVERSITY_STRATEGY: combined
```

**Your choice:**
```
DIVERSITY_STRATEGY: ___
```

---

## 4. CRITIQUE DIMENSIONS (Optional)

If you want specific aspects examined, list them. Otherwise, leave blank and the pipeline will auto-detect dimensions from your idea.

```
CUSTOM_DIMENSIONS:
-
-
-
```

---

## 5. AGENT NAMING (Optional)

Give your agents custom names for more engaging output. Leave blank for defaults (Advocate, Adversary, Judge, Synthesizer).

```
ADVOCATE_NAME: ___
ADVERSARY_NAME: ___
JUDGE_NAME: ___
SYNTHESIZER_NAME: ___
```

---

## 6. OUTPUT PREFERENCES

```
SAVE_ITERATIONS_TO_FILES: yes / no
FILE_FORMAT: md
GENERATE_PRESENTATION: yes / no
QUESTION_FORMAT: accept_improve_deny
```

---

## 7. DOMAIN CONTEXT (Optional)

Any domain-specific context the agents should know (e.g., "this is for the Qatar market", "B2B SaaS", "hardware product", "non-profit"). Helps agents ground their reasoning.

```
DOMAIN_CONTEXT: ___
```

---

## 8. CONSTRAINTS (Optional)

Hard constraints the pipeline should respect (e.g., "budget under $50K", "no external investors", "must work offline", "two-person team").

```
CONSTRAINTS:
-
-
```
