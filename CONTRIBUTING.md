# Contributing to gleam-ai

Thanks for contributing to **gleam-ai**. This guide covers org-wide expectations. Individual repositories may add project-specific steps in their own `CONTRIBUTING.md` or README.

## Code of Conduct

Participation is governed by our [Code of Conduct](./CODE_OF_CONDUCT.md). Be respectful and constructive.

## Ways to contribute

- Report bugs and propose features (use issue templates)
- Improve documentation
- Submit pull requests (fixes, features, tests, CI)
- Review PRs and help triage issues
- Improve security posture (see [SECURITY.md](./SECURITY.md))

## Development workflow

1. **Find or open an issue** — discuss larger changes before coding.
2. **Fork** (external) or branch from the default branch (members).
3. **Create a focused branch** using Conventional Commit prefixes:
   - `feat/<short-description>`
   - `fix/<short-description>`
   - `docs/<short-description>`
   - `chore/<short-description>`
   - `ci/<short-description>`
   - `refactor/<short-description>`
   - `perf/<short-description>`
   - `test/<short-description>`
4. **Keep PRs small** — one concern per PR when practical. Prefer <400 changed lines of reviewable code unless the change is inherently large (generated assets, renames).
5. **Open a pull request** early (draft is fine) using the PR template.
6. **Respond to review** from `@gleam-ai/maintainers` / `@gleam-ai/reviewers` and CI.

### Commit messages (Conventional Commits)

Use [Conventional Commits](https://www.conventionalcommits.org/) with an optional scope:

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

**Common scopes (Gleam):** `agent`, `webui`, `tools`, `harness`, `llm`, `ci`, `deps`, `docs`, `website`, `scripts`

Examples:

- `feat(agent): add plan re-score after tool failure`
- `fix(webui): prevent empty usage duration_ms`
- `docs(ci): document Windows test matrix`
- `chore(deps): bump actions/checkout to v7`

Breaking changes: add `!` after the type/scope (`feat(api)!: ...`) and a `BREAKING CHANGE:` footer.

### Signed commits and DCO-style sign-off

1. **SSH-signed commits** are required on protected branches. Configure:

   ```bash
   git config gpg.format ssh
   git config user.signingkey ~/.ssh/<your-signing-key>.pub
   git config commit.gpgsign true
   ```

2. **Sign-off** each commit (Developer Certificate of Origin style) with:

   ```bash
   git commit -s -S -m "feat(scope): description"
   ```

   The `-s` flag appends `Signed-off-by: Your Name <email>`. By signing off you certify that you have the right to submit the work under the project license.

Org maintainers committing as **vyrnsynx** must use the designated SSH signing key. Verify with `git log --show-signature -1`.

### Pull request size and review rules

| Size | Approx. diff | Expectation |
| --- | --- | --- |
| XS / S | <50 / <150 lines | Fast review |
| M | <400 lines | Standard review |
| L / XL | larger | Split when possible; call out why not |

- Link the issue (`Fixes #N` / `Closes #N`).
- Include tests for behavior changes.
- Update docs when user-visible behavior changes.
- Mark draft until ready; request review from `@gleam-ai/reviewers`.
- Resolve conversations before merge; stale approvals are dismissed on new pushes.
- Self-approval is not sufficient on protected branches — use admin merge only when CI is green and another maintainer path is unavailable.

### Local verification (Gleam)

Gleam is primarily **Go 1.22+** with embedded web UI and Python check scripts. On a Windows development machine (primary target):

```powershell
# Format + static + build + unit/integration tests
gofmt -l ./internal ./pkg ./cmd
go vet ./...
go build ./...
go test ./... -count=1 -timeout 300s

# Full six-layer gate (includes smoke + doctor/eval)
bash scripts/verify.sh --quick   # or full without --quick
```

See the product README and `scripts/verify.sh` for the authoritative gate.

### Release flow

1. Land changes on the default branch via reviewed PRs (linear history).
2. Conventional Commits drive **Release Drafter** changelog drafts (`release` label / merged PRs).
3. Maintainers cut a GitHub Release from the draft (or promote a tag). Binary artifacts follow the product packaging scripts / Release assets.
4. Hotfixes: `fix/` branch from the release tag, PR back to default branch, then patch release.

## Security

Do **not** file public issues for vulnerabilities. Follow [SECURITY.md](./SECURITY.md).

## License

By contributing, you agree that your contributions will be licensed under the same terms as the target repository (see that repo's `LICENSE`).
