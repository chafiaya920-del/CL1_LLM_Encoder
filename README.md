# CL1 LLM Encoder — Bio-Neural Language Model Integration

> **EXPERIMENTAL** — I am in no way associated with Cortical Labs or any research laboratory.

A research project investigating whether biological-style neural substrates can be tightly integrated with large language models to form a closed-loop bio-AI system — and whether such integration produces measurable evidence of functional coupling.

## Research Question

*Can a neural substrate (Izhikevich spiking model) be integrated tightly enough with an LLM that the closed-loop system produces falsifiable, statistically significant differences from decorrelated controls?*

## Key Findings (5-Experiment Series)

After 300-run confirmatory experiments across 3 independent random seeds:

| Metric | Bio-LLM | Shadow-LLM | Effect Size |
|--------|---------|-----------|-------------|
| Override rate | 1.6% | 7.5% | d = 1.40 ✅ |
| Neural-LLM alignment | **0.703** | 0.403 | d = **6.10** ✅ |
| Blended entropy | 2.68 | 2.96 | d = 3.26 ✅ |

**Result:** H0 rejected for functional integration (5/12 tests significant, p < 1e-16). The Bio-LLM closed loop is measurably distinguishable from both LLM-only and decorrelated Shadow-LLM controls.

**Not claimed:** Evidence of subjective experience or consciousness — functional integration is demonstrated, phenomenal integration is not.

## How It Works

```
Token → Spatial Encoder → 59-channel MEA stimulation
                                    │
                          Izhikevich neural substrate
                          (1000 neurons, STDP plasticity)
                                    │
                          Spike decoding → probability vector
                                    │
                    blend(α=0.5) with LLM logits → token selection
                                    │
                          Next token → feedback loop
```

The substrate learns via **STDP** (Spike-Timing Dependent Plasticity) to align its decoded probability distribution with the LLM's — confirmed by Neural-LLM alignment score of 0.703 (vs 0.403 in decorrelated control), the largest effect observed (Cohen's d = 6.10).

## Experimental Conditions

- **LLM-only (α=0):** Substrate measured but does not influence token selection
- **Bio-LLM (α=0.5):** Full closed loop with spatial encoder + STDP
- **Shadow-LLM (α=0.5):** Same as Bio-LLM but spike responses **shuffled** before decoding — breaks spatial consistency while maintaining identical stimulation (critical control)

## Substrate Configuration

- 1000 Izhikevich neurons (800 excitatory / 200 inhibitory)
- 59 channels (matching CL1 MEA layout)
- Balanced STDP (A_plus=0.005, A_minus=0.006) + homeostatic plasticity
- Spatial Encoder v2: Token ID → 8-channel stimulation via 64-dim embedding projection
- LLM: LFM2-350M (4-bit GGUF)

## Repository Structure

```
encoder_v3.py          — Spatial Encoder v3 (final)
cl1_experiment_v3.py   — Full closed-loop experiment runner
consciousness.py       — C-Score and consciousness metrics
analysis.py            — Statistical analysis pipeline
SCIENTIFIC_RESULTS.md  — Raw results across all 5 experiments
SCIENTIFIC_CONCLUSION.md — Full 9-section scientific report
```

## Run

```bash
pip install numpy scipy torch transformers llama-cpp-python
python run_experiment.py
```

## Honest Limitations

- Simulated neurons, not biological CL1 hardware
- Simplified pairwise STDP, not triplet/calcium-based
- Small LLM (350M params)
- IIT φ (integrated information) not computed
- Post-hoc hypothesis evolution in Experiments 1–2

Full analysis in [`SCIENTIFIC_CONCLUSION.md`](SCIENTIFIC_CONCLUSION.md).

## Next Steps

1. Port to real CL1 biological hardware (59-channel MEA)
2. Test with 7B+ parameter LLMs
3. Compute IIT φ for phenomenal integration evidence
4. Multi-session STDP persistence across 1000+ tokens

## License

MIT
