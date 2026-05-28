# sdk-generator

Reusable SDK generation pipeline for DigitalOcean SDKs.

This repo is the single source of truth for **how** SDKs get generated.
The SDK output repos (`godo-next`, `pydo-next`, `dots-next`) each call into
the reusable workflow here.

## Layout

```
fern/
  fern.config.json    # fern CLI version pin
  generators.yml      # one group per language, generator versions pinned
.github/workflows/
  generate.yml        # reusable workflow_call workflow used by all SDK repos
```

## Updating a generator

1. Bump the version in `fern/generators.yml`.
2. Open a PR. CI smoke-tests against a fixture spec (TODO).
3. Merge → the next spec-merge in `openapi-sdk` regenerates all SDKs with
   the new generator.

## Adding a new language

1. Add a new group to `fern/generators.yml`.
2. Create a new SDK output repo (e.g. `jdo-next` for Java).
3. Copy `.github/workflows/regen.yml` from an existing SDK repo, change
   the `language:` input.
4. Add the new repo to the fan-out matrix in `openapi-sdk/.github/workflows/dispatch.yml`.
