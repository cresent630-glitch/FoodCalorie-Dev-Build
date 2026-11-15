# FoodCalorie-Dev-Build

Public workflow-only builder for the private `cresent630-glitch/FoodCalorie-Dev` iOS source repository.

- Manual dispatch only (`Private iOS build`): input a full 40-character source commit SHA plus test/build options.
- Runs on the standard `xcode-27` GitHub-hosted macOS runner (free compute minutes for public repositories).
- Checks out private source with a read-only fine-grained PAT (`SOURCE_REPO_TOKEN`). Detailed logs, test results and the unsigned IPA are published only to the private `cresent630-glitch/FoodCalorie-Dev-Releases` repository via `PRIVATE_OUTPUT_TOKEN`.
- No source code, photos, keys or personal data are stored here. Public run pages show step status only.

Maintenance is restricted to trusted maintainers; review any workflow change before running private source. Tokens are fine-grained, repository-scoped and expiring; rotate them in GitHub Settings, never in chat or source.