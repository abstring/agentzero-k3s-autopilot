# agentzero-k3s-autopilot

Autopilot tooling for k3s using Agent Zero: assimilate nodes, run safe ops runbooks, and keep clusters healthy with GitOps.

## What this is
`agentzero-k3s-autopilot` is a set of **scripts, runbooks, and guardrails** that let [**Agent Zero**](https://github.com/agent0ai/agent-zero) safely operate a **k3s** cluster.

The goal is not “AI does whatever it wants.” The goal is **repeatable ops**:
- Node discovery + bootstrap (“assimilate”)
- Safe k3s join (worker or control plane)
- Health checks and triage
- Rolling upgrades
- GitOps-driven configuration and drift control

## What this is not
- Not a turnkey “one-click cluster” distro
- Not a replacement for Kubernetes fundamentals
- Not an excuse to give an agent unrestricted root + cluster-admin

## Key ideas
- **Least privilege by default**: tight RBAC, constrained sudo, no broad credentials
- **Idempotent operations**: scripts/runbooks over ad-hoc shell improvisation
- **Auditability**: actions should be explainable, loggable, and reproducible
- **No secrets in-repo**: examples only, bring your own tokens/keys

## Quick start (high level)
1. Run Agent Zero somewhere with reliable network access to your cluster (a “control host”).
2. Configure Agent Zero to use this repo as its “ops toolbox” (scripts + runbooks).
3. Provide:
   - A limited Kubernetes kubeconfig (RBAC-scoped)
   - SSH access to target nodes via a dedicated user (constrained sudo)
4. Use the runbooks:
   - `discover` → find new nodes
   - `assimilate` → baseline + join
   - `verify` → acceptance tests + labels/taints
   - `upgrade` → cordon/drain/upgrade/reboot/un-cordon

> This README will grow into concrete, copy/pasteable steps as the repo matures. For now, the emphasis is on laying down the patterns and safety model.

## Roadmap
- [ ] Minimal “assimilation” pipeline (discover → bootstrap SSH → baseline → join → verify)
- [ ] Reference RBAC manifests (read-only → limited-writes in a single namespace)
- [ ] Opinionated node labels/taints (including quarantine-on-join)
- [ ] Safe rolling upgrade runbook
- [ ] Example GitOps layout (kustomize/helm) with generic overlays
- [ ] Integrations (optional): UniFi visibility, Home Assistant alerts, Snipe-IT inventory

## Contributing
PRs welcome. If you’re planning anything non-trivial, open a Discussion first so we can align on:
- security posture
- naming conventions
- repo layout
- how to keep examples generic

## Licensing
Licensing: This project is licensed under the GNU Affero General Public License v3.0 (AGPL-3.0). If you modify this code and use it to provide a service over a network, you must make the complete corresponding source code of your modified version available to the users of that service, as required by the AGPL. See the LICENSE file for full terms.
