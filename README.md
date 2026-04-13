# Crucible

**Stress-test any idea through structured multi-agent debate.**

Crucible is a prompt-based pipeline that refines raw ideas using 4 AI agents with distinct reasoning strategies. No code to install — just prompts, templates, and a config file. Works with Claude, GPT-4, or any capable LLM.

```
Raw Idea → Advocate builds it → Adversary attacks it → Judge rules → You decide → Synthesizer assembles
```

## Why This Exists

Most people brainstorm ideas alone or get polite feedback from friends. Crucible puts your idea through a structured gauntlet:

- An **Advocate** builds and defends your idea using divergent thinking
- An **Adversary** attacks it along specific dimensions with evidence and precedent
- A **Judge** evaluates each dispute and surfaces the real decisions
- A **Synthesizer** assembles the final refined blueprint

The result: a version of your idea that has survived rigorous stress-testing, with every decision documented and every weakness addressed.

## Quick Start

### 1. Fill in the config

Copy `config.md` and fill in:
- Your idea (as messy or polished as you like)
- Number of iterations (6-10 recommended)
- How you want diversity introduced (see options below)
- Any constraints (budget, team size, market, etc.)

### 2. Start the pipeline

Open your LLM of choice (Claude, ChatGPT, etc.) and send this message:

```
I want you to run a structured ideation pipeline. Here are your instructions
and my configuration:

[paste contents of MASTER_PROMPT.md]

[paste contents of your filled-in config.md]
```

For best results with Claude: also paste the 4 agent files from `agents/` so the LLM has the full constitution for each agent.

### 3. The pipeline runs

The LLM will:
1. Plan which dimensions to debate (you approve the plan)
2. Run N iterations of structured Advocate vs. Adversary debate
3. Have the Judge rule on each disputed point
4. Present you with key decision questions (Accept / Improve / Deny)
5. Synthesize the final refined idea after your input
6. Run a validation pass to catch errors

### 4. You get the output

- One file per debate iteration (full transcript)
- A decision log with your choices
- A final blueprint document ready to act on

## Diversity Strategies

How Crucible introduces variation across iterations (pick one in config):

| Strategy | How It Works | Best For |
|----------|-------------|----------|
| **Dimension Rotation** | Each iteration attacks a different aspect (tech, revenue, market, etc.) | Most ideas. Comprehensive coverage. |
| **Perspective Shift** | Each iteration, the Adversary adopts a different stakeholder lens (investor, user, regulator, etc.) | Ideas with many stakeholders. |
| **Escalating Rigor** | Early iterations are constructive. Later ones are adversarial. Final iteration tries to kill the idea. | Testing resilience. |
| **Combined** | Dimension rotation + escalating rigor together. | Thorough analysis of complex ideas. |

> **Note on temperature/randomness:** Crucible does NOT rely on temperature for diversity. Research shows temperature is a weak lever — real diversity comes from structurally different prompts, reasoning strategies, and critique dimensions. Temperature is set per-agent as a secondary control (high for creative generation, low for precise critique).

## The 4 Agents

| Agent | Thinks Like | Temperature | Job |
|-------|------------|-------------|-----|
| **Advocate** | Divergent — analogies, reframing, "what if" | 0.8-1.0 | Build and defend the idea |
| **Adversary** | Convergent — evidence, precedent, failure modes | 0.2-0.4 | Structured critique along specific dimensions |
| **Judge** | Evaluative — weighs arguments, selects winners | 0.3-0.5 | Rule on disputes, surface decisions |
| **Synthesizer** | Integrative — structures, sequences, resolves | 0.2-0.3 | Assemble final blueprint |

Each agent has a **constitution** (explicit rules) and **anti-conformity instructions** to prevent premature agreement. See `agents/` for full details.

## Repo Structure

```
crucible/
  README.md              ← You're here
  LICENSE                ← MIT
  MASTER_PROMPT.md       ← The orchestration prompt (give this to the LLM)
  config.md              ← Fill this in with your idea + preferences
  DESIGN.md              ← Why the pipeline works this way (research-backed)
  agents/
    advocate.md          ← Advocate agent prompt + rules
    adversary.md         ← Adversary agent prompt + rules
    judge.md             ← Judge agent prompt + rules
    synthesizer.md       ← Synthesizer agent prompt + rules
  templates/
    iteration.md         ← Output format for each debate round
    questions.md         ← Output format for founder decision questions
    final_output.md      ← Output format for the final blueprint
```

## Design Principles

Crucible is built on multi-agent debate research (ICLR 2025, EMNLP 2024, NAACL 2024):

1. **Heterogeneous reasoning strategies** over different personas — agents differ in *how they think*, not who they pretend to be
2. **Structured critique dimensions** over open-ended feedback — the Adversary attacks specific axes, not everything at once
3. **2-3 debate rounds per iteration** — research shows diminishing returns after this
4. **Structural diversity over temperature randomness** — vary prompts and strategies, not just token sampling
5. **Selection-based judging** over synthesis-blending — the Judge picks winners, doesn't average
6. **Anti-conformity prompting** — both agents are instructed to resist premature agreement
7. **Final validation pass** — catches errors introduced during synthesis

For the full research basis and audit of the design, see [DESIGN.md](DESIGN.md).

## Tips

- **Start with 6-8 iterations** for a business idea. 3-5 for a feature or small concept.
- **Use Combined diversity strategy** for maximum thoroughness.
- **Name your agents** — it makes the output more engaging and easier to follow.
- **Add domain context** in the config — the more the agents know about your market, the sharper the critique.
- **List hard constraints** — "no investors", "two-person team", "under $50K" — these ground the debate in reality.
- **Don't skip the questions step** — your Accept/Improve/Deny decisions are what make the output truly yours, not a generic AI brainstorm.

## License

MIT — use it however you want.
