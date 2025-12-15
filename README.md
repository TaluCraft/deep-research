# Deep Research

**Turn any question into multi-agent exploration.**

```bash
./deep-research.sh "Why do smart people make bad decisions?"
```

One agent breaks your question into angles. Each angle gets its own researcher. Researchers can spawn more researchers. Results flow back up into a synthesis.

---

## See It In Action

```
You ask: "Why do startups fail?"
         │
         ▼
    Coordinator decides: "4 angles needed"
         │
         ├── Researcher 1 → Founder psychology
         ├── Researcher 2 → Market timing
         ├── Researcher 3 → Financial runway
         └── Researcher 4 → Team dynamics
                              │
                              └── Sub-researcher → Hiring mistakes
         │
         ▼
    Final synthesis combining all findings
```

Each agent asks itself: *"Can I answer this directly, or should I break it down further?"*

Same logic at every level. Unlimited depth. Stops when questions become simple enough to answer.

---

## Quick Start

```bash
git clone https://github.com/Cranot/deep-research.git
cd deep-research
chmod +x deep-research.sh

# Run it
./deep-research.sh "Your question here"
```

**Requires:** [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code)

---

## Example Reports

Real outputs from actual runs:

| Question | Config | Result |
|----------|--------|--------|
| [What makes great software architecture?](examples/software-architecture.md) | sonnet + haiku | 6 dimensions identified |
| [What is the key to learning fast?](examples/learning-fast.md) | sonnet + haiku | 5-principle framework |
| [Why do people self-sabotage?](examples/self-sabotage.md) | sonnet | Psychological deep-dive |
| [What makes people buy vs just admire?](examples/buy-vs-admire.md) | opus | Purchase psychology |

---

## Options

```bash
# Default: Opus orchestrator + Sonnet researchers
./deep-research.sh "Your question"

# Fast & cheap: Sonnet + Haiku
./deep-research.sh -m sonnet -r haiku "Your question"

# With web search (for current events)
./deep-research.sh --web "Latest developments in AI agents"

# Maximum depth: Sonnet + Sonnet (researchers can spawn more)
./deep-research.sh -m sonnet -r sonnet "Complex topic"
```

| Flag | What it does | Default |
|------|--------------|---------|
| `-m, --model` | Orchestrator model | opus |
| `-r, --researcher` | Researcher model | sonnet |
| `-w, --web` | Enable web search | off |

**Note:** Haiku researchers answer directly and won't spawn sub-researchers. Use `-r sonnet` if you want deeper recursion.

---

## Model Combinations

| Config | Depth | Speed | Cost | Best for |
|--------|-------|-------|------|----------|
| `-m opus -r sonnet` | Deep | Slow | $$$ | Best quality |
| `-m sonnet -r sonnet` | Deep | Medium | $$ | Good balance |
| `-m sonnet -r haiku` | Shallow | Fast | $ | Quick answers |

**Cost ranges:** $0.10-0.50 (sonnet+haiku) to $1-5 (opus+sonnet) to $5-15 (opus+opus+web)

---

## Output

Reports save automatically to:
```
reports/YYYY-MM-DD-your-question-slug/SYNTHESIS.md
```

---

## How It Works

The magic is one flag: `--allowedTools "Bash(claude:*)"`

This lets Claude spawn more Claude instances. Each instance gets the same "DNA":

```
Before answering, ask: are there multiple angles worth exploring?
- If YES → spawn sub-agents for each angle, wait, synthesize
- If NO → answer directly
Bias toward exploring. Go deep, not shallow.
```

That's it. Recursive by nature. Each agent can spawn more. The tree grows until questions become atomic.

---

## Built by

[AgentsKB](https://agentskb.com) - Pre-researched knowledge for AI agents

## License

MIT
