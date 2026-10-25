# Work Design Simulator

**Same AI, different job.** An interactive simulator that shows what happens to an HR operations team's performance, motivation and retention when AI is rolled out with or without redesigning the human job.

**Live demo:** https://12hourssip.github.io/work-design-simulator/

## What it does

A six-person HR Operations team handles employee letters and forms. An AI auto-issues the standard ones. The AI is identical in every scenario; only the coordinators' job design changes:

| Design | What the job becomes |
|---|---|
| **Before AI** | Each coordinator handles a request from intake to signed letter |
| **Automate only** | People handle only what the AI rejects; unusual cases escalate |
| **Automate + redesign** | People own cases end to end, tune the AI's rules and coach each other |

Each design is scored at 3 and 12 months on **volume, quality, motivation and retention risk**, and shown in a 3D office where you can tap any team member to see how their job changed.

## The model

Built on two work psychology frameworks, scored 1–7:

- **Job Characteristics Model** (Hackman & Oldham, 1976): skill variety, task identity, task significance, autonomy, feedback
- **Self-Determination Theory** (Deci & Ryan, 2000): autonomy, competence, relatedness

```
MPS            = (SV + TI + TS) / 3 × Autonomy × Feedback
Motivation     = 100 × (0.4 × MPS/343 + 0.6 × SDT/7)
Retention risk = 100 − Motivation
```

Every weight and constant can be changed in the **Model & settings** tab, and every score is shown step by step.

## Limits

This is a teaching and decision-support prototype, **not a validated forecasting tool**. Weights are set by theory-based reasoning, not estimated from data. To calibrate it, collect JCM/SDT survey scores and real outcomes (throughput, error rate, exits), estimate the weights by regression and enter them in the settings.

## Run it

It's a single `index.html` with no build step. Open it in a browser, or serve the folder with any static server. 3D uses [three.js](https://threejs.org/) r128 from a CDN.

## Credits

Concept, case design, framework choices and scoring logic by **Viann Wong** (MSocSc Industrial-Organisational Psychology). Interface and 3D office built with AI assistance (Claude).

### References

- Hackman, J. R., & Oldham, G. R. (1976). Motivation through the design of work: Test of a theory. *Organizational Behavior and Human Performance, 16*(2), 250–279.
- Deci, E. L., & Ryan, R. M. (2000). The "what" and "why" of goal pursuits: Human needs and the self-determination of behavior. *Psychological Inquiry, 11*(4), 227–268.
- Parker, S. K., & Grote, G. (2022). Automation, algorithms, and beyond: Why work design matters more than ever in a digital world. *Applied Psychology, 71*(4), 1171–1204.

## License

MIT
