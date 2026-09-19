## 1. Package quality

- [x] 1.1 Repair broken or non-granular skill references in the source package
- [x] 1.2 Add deterministic structure, link and TRACE gates with a 4.5 threshold
- [x] 1.3 Verify every skill and preserve generated evaluation evidence
- [x] 1.4 Replace the obsolete Codex-only consumer identity in both READMEs

## 2. Release dispatch

- [x] 2.1 Replace branch-driven or legacy dispatch with `release.published`
- [x] 2.2 Send package, release tag and peeled commit SHA to every current consumer
- [x] 2.3 Fail clearly when `SKILLS_SYNC_TOKEN` is unavailable or GitHub rejects the request

## 3. Publication

- [x] 3.1 Validate and archive the OpenSpec change
- [x] 3.2 Commit and push the skill package, then confirm CI
- [x] 3.3 Create immutable tag and GitHub Release `v1.0.2`
- [x] 3.4 Confirm consumer dispatch or record the exact secret-visibility blocker

> Blocked evidence: release run `35472192266` resolved `v1.0.2` but received an
> empty `SKILLS_SYNC_TOKEN` in the workflow environment and failed before
> dispatch. Tag and Release point to
> `8f2e5a7f2a1bd74f1db76a91ec8b621b60181ac0`.
