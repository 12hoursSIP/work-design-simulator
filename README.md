# Work Design Simulator

**Same AI, different job.** An interactive simulator that shows what happens to an HR operations team's throughput, quality, motivation and turnover when AI is rolled out with or without redesigning the human job.

**Live demo:** https://12hourssip.github.io/work-design-simulator/

## What it does

A six-person HR Operations team handles employee letters and forms. An AI auto-issues the standard ones. The AI is identical in every scenario; only the coordinators' job design changes:

| Design | What the job becomes |
|---|---|
| **Before AI** | Each coordinator handles a request from intake to signed letter |
| **Automate only** | People handle only what the AI rejects; unusual cases escalate |
| **Automate + redesign** | People own cases end to end, tune the AI's rules and coach each other |

Each design is scored at 3 and 12 months on **throughput, quality, motivation and turnover risk**, and shown in a 3D office where you can tap any team member to see their role, task and view before and after AI. A dashboard compares all three designs, and a short intro ("How it works") explains the setup.

## The model

Built on two work psychology frameworks, scored 1–7:

- **Job Characteristics Model** (Hackman & Oldham, 1976): skill variety, task identity, task significance, autonomy, feedback
- **Self-Determination Theory** (Deci & Ryan, 2000): autonomy, competence, relatedness

```
MPS         = (SV + TI + TS) / 3 × Autonomy × Feedback
Motivation  = 100 × (0.4 × MPS/343 + 0.6 × SDT/7)
Turnover    = 15% × (1 + (50 − Motivation)/50)          yearly, shown as expected leavers out of 6
Throughput  = (AI 80 | manual 55) + 0.75 × (7 − Autonomy) − 0.1 × Feedback
              − vacancy loss (0.5 × turnover) − 3-month learning dip (1% per new skill point)
Quality     = (AI 82 | manual 80) + 12 × (0.35·TI + 0.35·FB + 0.3·Competence)/7
              − 0.1 per % turnover − 3-month learning dip (0.4 per new skill point)
```

Every weight and constant can be changed in the **Model & settings** tab, and every score is shown step by step. 24 built-in checks run on load.

### Results (model v2, defaults)

| Index | Before AI | Automate only 3m | Redesign 3m | Automate only 12m | Redesign 12m |
|---|---|---|---|---|---|
| Throughput (0–100) | 52.7 | **81.1** | 72.7 | 74.8 | **76.0** |
| Quality (0–100) | 85.6 | 87.1 | **88.3** | 85.6 | **90.7** |
| Motivation (0–100) | 42.0 | 30.9 | **65.3** | 30.9 | **65.3** |
| Turnover risk (%) | 17.4 | 5.6 | **2.7** | 20.7 | **10.4** |

Automate only wins throughput in the first quarter while the redesigned team learns new work. By 12 months, twice as many people have left the Automate only team and Redesign leads on every outcome.

## v2: how the model was corrected

The original model (v1) is still available as a switch in **Model & settings**. A critical review against the research led to these changes:

| Problem in v1 | Fix in v2 |
|---|---|
| "Before AI" was scored with the AI's capacity and accuracy | Manual baselines (throughput 55, quality 80) |
| Retention risk = 100 − motivation, too strong (satisfaction–turnover r ≈ −.2, Griffeth et al., 2000) | Realistic yearly turnover from a 15% base, shown as expected leavers out of 6 |
| Quality effect of job design too large (weak link to objective performance, Humphrey et al., 2007) | Human effect on quality cut from 30 to 12 points |
| Automate only scored near the floor | Fairer profile, mostly 3s |
| No learning curve | 3-month dip scaled to how many new skills the redesigned job needs |
| Autonomy counted twice with identical values | Job autonomy and felt autonomy now differ in the defaults |

Each metric also shows a likely-range band (all inputs ±0.5).

## Limits

This is a teaching and decision-support prototype, **not a validated forecasting tool**. Inputs and weights are reasoned estimates, not data. The model leaves out headcount cuts, training cost, governance of AI rule changes, job insecurity, pay and the job market. To calibrate it, collect JCM/SDT survey scores and real outcomes (throughput, error rate, exits), estimate the weights by regression and enter them in the settings.

## Run it

It's a single `index.html` with no build step. Open it in a browser, or serve the folder with any static server. 3D uses [three.js](https://threejs.org/) r128 from a CDN.

## Credits

Concept, case design, framework choices and scoring logic by **Viann Wong** (MSocSc Industrial-Organisational Psychology). Interface and 3D office built with AI assistance (Claude).

### References

- Hackman, J. R., & Oldham, G. R. (1976). Motivation through the design of work: Test of a theory. *Organizational Behavior and Human Performance, 16*(2), 250–279.
- Deci, E. L., & Ryan, R. M. (2000). The "what" and "why" of goal pursuits: Human needs and the self-determination of behavior. *Psychological Inquiry, 11*(4), 227–268.
- Griffeth, R. W., Hom, P. W., & Gaertner, S. (2000). A meta-analysis of antecedents and correlates of employee turnover. *Journal of Management, 26*(3), 463–488.
- Humphrey, S. E., Nahrgang, J. D., & Morgeson, F. P. (2007). Integrating motivational, social, and contextual work design features: A meta-analytic summary and theoretical extension of the work design literature. *Journal of Applied Psychology, 92*(5), 1332–1356.
- Parker, S. K., & Grote, G. (2022). Automation, algorithms, and beyond: Why work design matters more than ever in a digital world. *Applied Psychology, 71*(4), 1171–1204.

## License

MIT
