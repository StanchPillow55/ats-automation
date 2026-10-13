# Contributing

Thanks for helping keep Resume Curator auditable. The useful change is one that makes a requirement's coverage easier to trust, not one that makes the resume sound stronger than the evidence.

## Ways to contribute

| Kind of work | Where to start |
|---|---|
| Bug in matching, selection, or verification | [Bug report](.github/ISSUE_TEMPLATE/bug_report.md) |
| New fixture or role-family JD | [TO_DO.md](TO_DO.md) → Good first contributions |
| Benchmark / labeled case | [Benchmark case](.github/ISSUE_TEMPLATE/benchmark_case.md) |
| Feature idea | [Feature request](.github/ISSUE_TEMPLATE/feature_request.md) |
| Security or privacy issue | [SECURITY.md](SECURITY.md) (private advisory; no public real resumes) |

Open source contributions are welcome via GitHub issues and pull requests against [hoplitetechsjsu-lab/ats-automation](https://github.com/hoplitetechsjsu-lab/ats-automation). Fork the repo if you do not have push access, push your branch to your fork, and open a PR into `main` (or the active feature branch maintainers are using).

## Setup

Node.js 22 or newer.

```bash
npm install
npm test
npm run lint
npm run typecheck
npm run dev
```

The review UI is at `http://127.0.0.1:3847` after `npm run dev`.

Offline compile (same inputs → same hashes and PDF bytes):

```bash
npm run compile -- --jd fixtures/sample-backend.jd.txt --out output/sample
```

## Ground rules

- Do not commit real resumes, contact details, confidential research, or private job descriptions. `fixtures/` is synthetic on purpose.
- Do not add a model call to the default path. Exact and alias matches are the coverage authority. Suggestions must stay labeled as suggestions.
- Do not invent aliases in code. Add them to the skill table in a fixture or to a reviewed vocabulary, with ambiguous short forms marked.
- A change that lets planned work, negated text, or an untagged skill count as verified coverage needs a failing test first, then a fix that keeps the test.
- Keep scoring weights in `config/compiler.json`. Say what the weight change does to the fixtures.
- Prefer small PRs: one behavior change, one fixture, clear test coverage.

## First-time contribution path

1. Skim [README.md](README.md) and the open items in [TO_DO.md](TO_DO.md).
2. Pick a **Good first contribution** or a labeled issue.
3. Branch from the latest `main` (or the branch named in the issue).
4. Add a synthetic job description or library tweak under `fixtures/` and lock the expected coverage states in `tests/compiler.test.ts`.
5. Run `npm test`, `npm run lint`, and `npm run typecheck`.
6. Open a pull request using [.github/PULL_REQUEST_TEMPLATE.md](.github/PULL_REQUEST_TEMPLATE.md). Link the issue or TO_DO bullet.

Useful cases to add:

- a must-have the library truly supports
- a must-have it must leave uncovered
- negation, exposure-only language, and instruction-like text
- an ambiguous alias such as `Go` versus the verb "go", or `Java` versus `JavaScript`

Prefer a small labeled case over a new subsystem.

## Pull requests

- Describe the behavior change and the fixture that locks it in.
- Check every box in the PR template that applies.
- Do not include generated resumes from `output/` or anything from a real application.
- If your change adds optional AI or network access, keep it behind an explicit flag and out of the default path; document the provider boundary in the PR.

## Code of conduct and security

See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md). Report security or privacy issues through the process in [SECURITY.md](SECURITY.md).

## License

By contributing, you agree that your contributions are licensed under the MIT License in [LICENSE](LICENSE).
