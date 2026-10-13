# To-do

Roadmap for Resume Curator against the design contract: a local, deterministic, evidence-preserving resume compiler. Items marked done are already in this repository. Pick open items that keep provenance and reproducibility intact.

Design reference (local): `../ats-semantic-resume-curator-design-spec.md` if you have the companion spec file next to this checkout.

## Done (Phase 1 MVP)

- [x] Clean-room MIT implementation (not a fork of GPLv3 `ats-tailor`)
- [x] YAML evidence library with claims, skills, aliases, ownership, and approved variants
- [x] Pasted JD input with deterministic requirement extraction
- [x] Exact and alias matching; lexical overlaps labeled as suggestions only
- [x] Requirement-to-claim coverage ledger with source ids
- [x] One-page HTML/PDF render plus separate readability, coverage, and density checks
- [x] Pins, exclusions, human edits with unsupported-claim refusal
- [x] Adversarial fixtures (negation, planned work, ambiguous aliases, instruction-like text)
- [x] Reproducible CLI compile (`report.json`, `coverage.md`, `resume.html`, `resume.pdf`)
- [x] Local review UI and OSS surfaces (README, CONTRIBUTING, CoC, SECURITY, templates, CI)

## Good first contributions

Small, reviewable changes. Prefer a fixture + test over a new subsystem.

- [ ] Add synthetic JDs for frontend, infra/SRE, data/ML, security, and intern role families under `fixtures/`
- [ ] Expand ambiguous-alias cases (`Go` vs verb “go”, `Java` vs `JavaScript`, short forms marked ambiguous)
- [ ] Document a walkthrough of reading `report.json` and the coverage ledger in `CONTRIBUTING.md` or the README
- [ ] Improve empty/error UI copy when a JD has only soft or ignore lines
- [ ] Add a “how to propose a skill alias” issue template checklist that points at the fixture skill table

## Next (Phase 2–3)

Keep the default path model-free. Anything semantic must stay in the suggestion channel until a human accepts it.

- [ ] Optional local Sentence Transformer retrieval behind a feature flag (pinned model version + embedding cache)
- [ ] Show semantic-only candidates as “review suggested,” never as verified coverage
- [ ] Ablation notes: exact-only vs exact+alias vs exact+alias+semantic on fixtures
- [ ] Persist run history locally (config hash, report hash, timestamps) without logging raw contact fields
- [ ] Library editor UX: approve aliases, pin/exclude, accept/reject variants without leaving the review UI
- [ ] DOCX export with the same verification checks as PDF (optional)

## Later (Phase 4–5)

- [ ] Optional local LLM JD span proposals with schema validation, prompt/version hashes, and human accept/reject
- [ ] Diff view for proposed bullet variants; no write-back to the library without explicit approval
- [ ] Cover letter draft from selected evidence + one user-authored motivation sentence; every line traced or marked user-authored

## Evaluation harness

- [ ] Labeled benchmark of 30–50 synthetic/redacted JDs with requirement spans, kinds, and acceptable claims
- [ ] Metrics scripts: extraction F1, match precision/recall, unsupported-claim rate (target 0), page-fit pass rate
- [ ] Inter-annotator agreement on a subset of cases; surface uncertainty in the UI rather than a false precision score

## Explicitly not to-do (for now)

Do not open PRs that add these to the default path without a design discussion:

- Interview-probability or employer “ATS score” predictors
- Job-board scraping or auto-submit
- Silent generative rewrites or inventing skills/metrics/ownership
- Uploading the evidence library to a remote model by default
- Committing real resumes, phone numbers, or confidential postings

## Working on an item

1. Open or claim an issue (or note the TO_DO bullet in your PR).
2. Follow [CONTRIBUTING.md](CONTRIBUTING.md).
3. Add or extend a synthetic fixture and assert behavior in `tests/compiler.test.ts`.
4. Run `npm test`, `npm run lint`, and `npm run typecheck` before opening the PR.
