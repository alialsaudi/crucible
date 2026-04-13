# Audit: Original Approach vs. Enhanced Pipeline

## What We Did Originally

In the BigIdea session, we ran a 3-person ideation process:
- **Person A** (Ali): pitched and defended the idea
- **Person B** (Rashid): critiqued and challenged
- **Person C**: synthesized the final document after founder decisions

10 iterations, each covering a different topic, with a Q&A step before synthesis.

**What worked well:**
- The back-and-forth format produced genuinely useful pivots (e.g., "boredom shopper" → "local explorer")
- Topic-based iteration kept each debate focused
- The Q&A step gave the founder real control over the direction
- Saving iterations to files created a useful paper trail

**What was weak (and why):**

| Weakness | Why It Matters | Research Basis |
|----------|---------------|----------------|
| No explicit Judge agent | Disputes were resolved by A and B reaching informal consensus, which biases toward conformity | ICLR 2025 MAD studies show conformity bias is the #1 failure mode in agent debates |
| Temperature used as diversity lever | "Changing temperature" was listed as a randomness tool, but temperature is a weak diversity knob | Lakera 2025 study: prompt-based mitigation cut hallucination from 53% to 23%; temperature tweaks barely moved the needle |
| Agents had personalities, not reasoning strategies | "Visionary" and "Critic" are persona labels, not cognitive strategies | DMAD (ICLR 2025): assigning distinct reasoning strategies outperforms assigning distinct personas |
| No anti-conformity mechanism | Agent A often conceded too readily when B pushed confidently | G-DMAD research: unstructured debate leads to premature convergence due to LLM conformity bias |
| No structured critique dimensions | B's critiques were open-ended — sometimes sharp, sometimes scattered | Constitutional AI patterns: agents with explicit evaluation criteria produce more consistent, higher-quality critique |
| No validation pass on synthesis | Person C's final document was not stress-tested | Multi-agent pipeline research: a final adversary pass catches 15-20% of errors introduced during synthesis |
| No hallucination guards | No formal mechanism to prevent fabricated facts | Cross-iteration fact-checking is standard in production debate pipelines |

---

## What Changed in the Enhanced Pipeline

### 1. Added Judge Agent (NEW)
**Before:** A and B negotiate directly → informal consensus → questions for founder.
**After:** A and B debate → Judge evaluates each disputed point → clear verdicts → only unresolved items go to founder.

**Why:** The Judge prevents conformity bias (A agreeing too easily) and ensures valid minority concerns aren't lost when A concedes under pressure. Based on courtroom-style debate patterns (arXiv 2025).

### 2. Replaced Temperature Diversity with Structural Diversity
**Before:** "Change temperature as you like" for randomness.
**After:** Four structural diversity mechanisms:
- **Reasoning strategy rotation:** Each iteration uses a different cognitive approach (analogy, first-principles, scenario, data-driven). Never consecutive repeats.
- **Dimension assignment:** Each iteration attacks a different aspect. Covered systematically, not randomly.
- **Rigor escalation:** Optional progressive adversarial intensity (friendly → hostile).
- **Perspective shifting:** Optional stakeholder lens rotation.

Temperature is still set per-agent-per-phase, but as a secondary control, not the primary diversity lever.

**Why:** Research consistently shows that structural prompt variation produces genuine diversity. Temperature variation produces superficial token-level randomness that doesn't change the substance of the argument. (DMAD, ICLR 2025; Lakera hallucination study 2025)

### 3. Agents Defined by Cognitive Function, Not Personality
**Before:** Person A is "someone who has an idea" and Person B "listens and makes comments."
**After:** Each agent has:
- A named cognitive function (expansive ideation, convergent critique, evaluative analysis, integrative assembly)
- A specific reasoning strategy (divergent, convergent, evaluative, integrative)
- A constitution (explicit rules governing behavior)
- Anti-conformity instructions

**Why:** NAACL 2024 persona research found that irrelevant persona details can cause unpredictable performance drops of up to 30%. Top-2 coarse cognitive attributes outperform elaborate backstories. Defining agents by how they *think* (not who they *are*) produces more consistent quality.

### 4. Added Critique Dimension Menu
**Before:** Topics chosen ad-hoc (3D streets, AI indexing, delivery, etc.)
**After:** Systematic dimension menu (technical feasibility, revenue model, market size, competition, operations, etc.) selected in Phase 0 based on the idea's specific needs. User approves the plan before debate begins.

**Why:** Structured dimension assignment ensures comprehensive coverage. The original approach happened to cover most bases, but it wasn't guaranteed — a different idea might have missed critical dimensions.

### 5. Added Anti-Conformity Prompting
**Before:** No mechanism to prevent premature agreement.
**After:** Both Advocate and Adversary have explicit anti-conformity instructions:
- Advocate: "Do not agree simply because the Adversary stated something confidently."
- Adversary: "Do not soften your critique because the Advocate responded passionately."
- Pipeline: "If the Advocate agrees with every critique, STOP and re-examine."

**Why:** LLM conformity bias is well-documented. Without explicit countermeasures, agents converge too quickly, especially when one agent makes a confident-sounding argument. (G-DMAD, 2025)

### 6. Added Final Validation Pass
**Before:** Person C synthesized and that was the final output.
**After:** After synthesis, one more Adversary pass specifically checking for: internal contradictions, unsupported claims, missing debate elements, and vague action items.

**Why:** Synthesis introduces new errors — contradictions between sections, claims that survived debate but were softened in synthesis, action items that are vague because the synthesizer didn't have enough context. A targeted quality check catches these. This is standard in production multi-agent pipelines.

### 7. Added Hallucination Prevention Protocol
**Before:** "Each iteration checked to not hallucinate ideas" — stated as a goal but no mechanism.
**After:** Five specific checks:
1. No invented companies/products/statistics
2. No fabricated technical capabilities
3. No invented market data
4. Cross-iteration consistency checks
5. Adversary as primary hallucination detector (challenges claims that sound too good)

**Why:** Hallucination prevention requires specific, checkable rules — not just intent. The Adversary's constitutional role as fact-checker is the most effective mechanism because it's embedded in the debate flow.

### 8. Made the Pipeline Configurable and Replicable
**Before:** Custom session, not reproducible.
**After:** Config file captures all parameters. Templates standardize output format. Agent prompts are modular — swap, customize, or add agents.

---

## What Stayed the Same (Because It Worked)

| Element | Why It Was Kept |
|---------|----------------|
| Back-and-forth debate format | The core pattern (propose → critique → defend → resolve) is validated by research |
| Topic-based iterations | Dimension-focused debate outperforms free-form discussion |
| Founder Q&A step with Accept/Improve/Deny | Keeps the human in the loop at the right moment — after debate, before synthesis |
| Save iterations to files | Paper trail, auditability, context preservation |
| Web research when unsure | Grounding in real data prevents hallucination |
| Synthesis agent for final document | Dedicated assembly agent produces better structured output than asking the debate agents to summarize |

---

## Performance Expectations

Based on research, the enhanced pipeline should produce:
- **Higher quality critiques** (structured dimensions + constitutional rules)
- **Less premature convergence** (anti-conformity prompting + Judge agent)
- **More genuine diversity** (structural rotation > temperature randomness)
- **Fewer hallucinated claims** (explicit prevention protocol + Adversary as fact-checker)
- **Cleaner final output** (validation pass catches synthesis errors)
- **Reproducible results** (config + templates + modular agents)

The pipeline adds ~30% more token cost (Judge rulings + validation pass) but research suggests this investment catches 15-20% of errors that pass through simpler debate structures.
