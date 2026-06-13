# Debate to Priors

Most debates are unproductive not because people argue badly, but because they're arguing about the wrong thing.

Two people debate the ethics of life extension. One cites studies on social inequality, the other cites studies on human flourishing. They go back and forth for an hour and nobody moves. What's actually happening: one person holds an intuition — almost pre-rational — that there is something right about the natural life cycle, that death gives life its shape, that circumventing it violates something sacred. The other holds a different intuition: that life is the supreme value, and more of it is always better. Neither person has stated this. They're both trying to win a factual argument that is actually downstream of a value axiom neither has named.

This is the problem Debate to Priors is built to solve.

---

## The core idea

Every argument has two layers:

**The surface layer** — the claims, evidence, and logic each person actually says out loud. This is where most debate happens.

**The prior layer** — the implicit probability assignments and value weights that make the surface arguments feel obvious or wrong to each person. This is where most disagreements actually live.

When two people share the same priors, they will usually reach the same conclusions given the same evidence. When they diverge, no amount of evidence-trading will close the gap — because each side is filtering evidence through different priors and arriving at the same positions they started with.

The tool does one thing: it lifts the debate off the surface layer and shows you the prior layer. It extracts the implicit confidence each person assigns to shared claims, surfaces the magnitude of the gap, classifies whether the disagreement is empirical (a factual dispute that evidence could resolve) or normative (a value dispute that evidence cannot resolve), and then — crucially — proposes the minimum belief updates each party would need to make for consensus to be reachable.

---

## Why this is hard to replicate by just asking an LLM

The obvious objection: can't you just drop two arguments into ChatGPT and ask "what's the fundamental disagreement here?"

You can. You'll get a reasonable summary. But that's not the same thing, for a few reasons:

**Summaries describe. This maps.** A summary tells you what each person thinks. A prior map tells you *where the gap is* and *how large it is* — not in words, but as a structured, comparable object. The gap between "Person A assigns 20% confidence to this claim and Person B assigns 85%" is quantitatively different from "they disagree on this." The magnitude matters. A 65-point prior gap on an empirical claim is a resolvable disagreement — point them at the evidence. A 30-point gap on a normative claim is not resolvable by evidence — naming that is itself the useful output.

**It separates empirical from normative.** This distinction is philosophically load-bearing. Empirical disagreements have in-principle resolutions: better data, better studies, clearer definitions. Normative disagreements don't — they're about values, and values aren't true or false. If you're in an immortality debate and the model tells you "your core gap is on the normative claim that natural death has intrinsic value," you now know you're not in a factual argument. That realization changes everything about how the conversation should proceed.

**It names blind spots — the claims neither person made.** Some of the most important premises in an argument are the ones nobody states because both parties assume them — or assume the other person doesn't hold them. Surfacing these is often the most valuable part of the analysis.

**It suggests resolution paths.** Not "here's who's right," but "here's the minimum update each party would need to make, and here's the evidence or argument that could justify it." The tool doesn't adjudicate. It maps the territory and shows where the road could be built.

---

## The moat

The moat is not technical. Any good LLM can extract claims. The moat is the framing — the Bayesian epistemology layer that turns a debate into a structured object you can reason about.

Specifically:

1. **Quantified prior gaps, not qualitative summaries.** The output is a map with numbers. You can see at a glance which disagreement is largest, and whether it's empirical or normative.

2. **The empirical/normative split as a first-class output.** This is what tells you whether evidence can help or not. Most debate tools don't make this distinction. It's the most important distinction in epistemology.

3. **Audio-first, real-time.** Arguments captured live — from an actual conversation, not a written essay — are messier, more honest, and more revealing. The voice transcription pipeline lets you drop this into a real debate in progress.

4. **Resolution suggestions that don't take sides.** The tool tells you what each person would need to update to reach agreement, and by how much. It doesn't say who's right. It says what the gap is and what it would take to close it. That's a fundamentally different and more useful output than a verdict.

The long-term version of this sits inside every negotiation, every policy debate, every persistent argument people have with family members over dinner. The value is not in the analysis — it's in the moment of recognition when someone sees their own unstated prior written out and says "oh. *that's* what I actually believe."

---

## Files

| File | Description |
|---|---|
| `debate_to_priors_ollama.html` | Runs locally against any Ollama model. No API key needed. Set your Ollama URL and model in the config bar. Requires Ollama running with CORS enabled: `OLLAMA_ORIGINS=* ollama serve` |
| `debate_to_priors_anthropic.html` | Runs against the Anthropic API. Paste your API key into the config bar. Uses Claude Sonnet by default; Haiku and Opus also selectable. |

Both files are single HTML files — no build step, no dependencies, open in a browser.

---

## What the output contains

**Claims extracted per person** — 4–7 atomic propositions inferred from each argument, each with an implicit confidence level (0–100%) and a type tag: `empirical` or `value`.

**Prior gaps** — the claims both parties address, sorted by gap magnitude. A 65-point gap means one person assigns 15% confidence and the other assigns 80%. That's the disagreement. Gaps are color-coded: red for core disagreements (≥45pp), amber for notable gaps (25–44pp), green for minor gaps (<25pp).

**Blind spots** — 2–4 premises implied by both positions but stated by neither. Often the most revealing section.

**Resolution paths** — for the top 3 gaps, specific proposals: what each person would need to update, the direction and rough magnitude of the shift, and concrete evidence or arguments that could justify it. If the evidence clearly favors one side, the tool says so — it doesn't manufacture false symmetry.

**Summary** — 2–3 sentences on what the disagreement is really about at the level of world models.

---

## How to use it

**Text mode** — paste or type each person's argument into the text boxes. Works well for written arguments, articles, essays, comment threads.

**Voice mode** — click the mic button under each person's box and speak. The transcript appears in real time. Works well for capturing live conversations, recorded audio played back, or spoken summaries of a position.

Hit **Analyze disagreement**. The model runs the full analysis and renders the map below.

---

## Caveats

The confidence assignments are inferred, not measured. The model is making educated guesses about implicit beliefs based on word choice, hedging, and argument structure. These are useful approximations, not ground truth.

The empirical/normative classification is also a model judgment and will sometimes be wrong or contested. Some claims sit at the boundary — treat the classification as a starting point for reflection, not a verdict.

The tool surfaces disagreements; it doesn't resolve them. That's intentional. The resolution paths are suggestions, not prescriptions. The point is to give both parties a shared map of the disagreement so they can decide together what to do with it.

---

## Built with

- Vanilla HTML/CSS/JS — no framework, no build step
- Web Speech API for voice transcription (Chrome/Edge; falls back gracefully)
- Ollama (local) or Anthropic API for the analysis
- Prompted as an analytic philosopher and Bayesian epistemologist

---

## Roadmap ideas

- **Side-by-side debate mode**: real-time turn-by-turn analysis as a conversation unfolds, updating the prior map after each exchange
- **Prior update tracking**: if the same two people run the tool multiple times, track how their priors shift over time
- **Shared output link**: generate a shareable URL containing the analysis so both parties can see the same map
- **Calibration feedback**: after the debate resolves (or doesn't), let participants rate how accurate the prior extraction was — dataset for fine-tuning
- **Multi-party debates**: three or more positions, showing a full prior graph rather than a pairwise comparison
