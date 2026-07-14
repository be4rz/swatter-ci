# swatter-ci

Central [Swatter](https://github.com/lohi-ai/swatter) review config for all my
repos. Each repo carries only a small stub workflow; every setting that matters
(gateway URL, models, effort) lives in
[`.github/workflows/review.yml`](.github/workflows/review.yml) here, so changes
apply everywhere at once.

## Add Swatter to a repo

1. Copy [`stub.yml`](stub.yml) to `.github/workflows/swatter.yml` in the repo.
2. Set the API key secret: `gh secret set SWATTER_API_KEY -R <owner>/<repo>`

## How reviews trigger (on-demand mode)

- A PR gets one automatic review when opened or reopened.
- After that, comment `@swatter review` on the PR to re-review (owner and
  collaborators only).
- Reviews are advisory (`fail_on: never`): inline comments + summary + a green
  check, never a blocked merge.

## Backend

Model calls go to a self-hosted [9router](https://github.com/decolua/9router)
gateway (EC2, HTTPS) backed by a Codex subscription. This repo contains no
secrets — the gateway rejects calls without the API key, which lives only in
each repo's encrypted Actions secrets.
