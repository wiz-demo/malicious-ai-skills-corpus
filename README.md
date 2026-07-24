# malicious-ai-skills-corpus

Private mirror of a pinned subset of the [DataDog
malicious-software-packages-dataset](https://github.com/DataDog/malicious-software-packages-dataset)
corpus (`samples/ai-skills/malicious_intent/`), used by
[`wiz-demo-infra`](https://github.com/wiz-demo/wiz-demo-infra)
`scenarios/scenario89/aws` (SHOW-846) to stage malicious AI skill packages on
demo EC2 instances for the Wiz disk scanner to hash-match.

This repo exists so that scenario89's `terraform apply` / instance boot
never depends on the upstream DataDog repo's availability at runtime — we
own this copy and control when/whether it changes.

- **Upstream source**: https://github.com/DataDog/malicious-software-packages-dataset
- **Upstream commit mirrored**: `ae9592290339cc0ab281b6e58c3cf6fb3c0b6ed2`
- **Contents**: the 45 skill packages referenced by scenario89's
  `dev_agent_skills` / `content_agent_skills` / `devops_agent_skills` locals,
  preserving the upstream `samples/ai-skills/malicious_intent/<skill>/<skill>.zip`
  layout so scenario89's cloud-init sparse-checkout logic is unchanged aside
  from the repo URL.
- **Contents are inert**: these are zipped files only; nothing in this repo
  or in scenario89 executes them.

## Updating

To mirror a newer upstream commit or add/remove skills, re-run the same
sparse-checkout-and-push procedure documented in
`scenarios/scenario89/aws/README.md` of `wiz-demo-infra`, then bump
`malicious_corpus_commit_sha` there once this repo's `main` is confirmed
green.
