# Governance

## Purpose

This document describes how **gleam-ai** makes decisions, who maintains repositories, and how roles change.

## Roles

| Role | Who | Responsibilities |
| --- | --- | --- |
| **Org admin** | GitHub org owners (currently includes `vyrnsynx`) | Billing/settings, teams, rulesets, app installs |
| **Maintainer** | Members of `@gleam-ai/maintainers` | CODEOWNERS, merges to protected branches, releases, security triage |
| **Reviewer** | Members of `@gleam-ai/reviewers` | PR review, issue triage assistance |
| **Contributor** | Anyone submitting issues/PRs | Follow CoC, CONTRIBUTING, DCO-style sign-off |

## Decision making

1. **Day-to-day technical decisions** — maintainers of the affected repository, via PR review.
2. **Cross-repo / org policy** — proposed in an issue or PR against `gleam-ai/.github`, decided by maintainers (lazy consensus; silence after a reasonable period counts as assent).
3. **Security emergencies** — any maintainer may act immediately, then document the change.
4. **Disputes** — escalate to org admins; final call rests with org admins.

## CODEOWNERS

Product repositories list `@gleam-ai/maintainers` (and optionally `@vyrnsynx`) in `CODEOWNERS`. Required reviews are enforced via repository rulesets.

## Adding or removing maintainers

1. Open an issue in `gleam-ai/.github` proposing the change.
2. Existing maintainers discuss (publicly when possible).
3. An org admin updates the GitHub team membership.

## Changes to this document

Amend via pull request to this repository. Significant changes should be announced in a tracking issue.
