# plato-codex-run

Plato's pinned Codex runner workflow (reusable GitHub Actions workflow). No secrets or customer data.

## What it is

`.github/workflows/codex-run.yml` is a reusable workflow (`on: workflow_call` only, no other triggers). A repository that
uses Plato with Codex holds one small caller file that runs this workflow when its owner asks for a Codex change. The
workflow gets a short-lived key from Plato at the start of the run, runs Codex with it, gives the key back at the end,
and opens a branch with the result.

## No secrets

This repository holds no secret, key or customer data, and the workflow reads no repository secret. The short-lived run
key is exchanged at run time from GitHub's own identity token. Every action it uses is pinned by full commit sha.

## Callers pin it by full SHA

A caller must name this workflow by the full 40-character commit sha, never a branch or a tag:

    uses: augmentation-co/plato-codex-run/.github/workflows/codex-run.yml@<full commit sha>

Plato checks that sha in the run's token and refuses a run that uses any other. Changes here go through a pull request
and a new sha; each new release asks the repositories that use it to update their one file.
