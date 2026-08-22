# Maintaining this fork

This fork is a compatibility bridge for `ai-sdk-ollama`, not an independent
redesign of the Ollama JavaScript client.

## Branches

- `main` mirrors `ollama/ollama-js`.
- `maintained-v0.6.4` contains the reviewed patches shipped by this fork.
- Release tags use `vX.Y.Z-maintained.N` and publish the matching npm version.

## Included patches

| Upstream PR | Behaviour | Why it is included |
| --- | --- | --- |
| [#281](https://github.com/ollama/ollama-js/pull/281) | Completion-only streaming fields are optional | Matches intermediate NDJSON chunks |
| [#284](https://github.com/ollama/ollama-js/pull/284) | Maps `maxResults` to `max_results` | Matches the Ollama web-search wire format |
| [#288](https://github.com/ollama/ollama-js/pull/288) | Accepts a per-request `AbortSignal` | Allows AI SDK cancellation to reach fetch |

## Patch policy

1. Base every maintained branch on a named upstream commit.
2. Include only patches covered by tests and needed by `ai-sdk-ollama`.
3. Link every fork-only change to an upstream issue or pull request.
4. Prefer upstream fixes and remove fork patches after upstream releases them.
5. Track parity against the Ollama HTTP protocol, not language-specific Python
   conveniences.

## Release checklist

1. Sync `main` from `ollama/ollama-js`.
2. Rebase a new maintained branch and re-apply still-needed patches.
3. Run `npm ci`, `npm run lint`, `npm test`, and `npm run build`.
4. Test the packed artifact with both root and `./browser` imports.
5. Create a prerelease such as `v0.6.4-maintained.0`.
6. Pin `ai-sdk-ollama` to the exact published version using an npm alias.

