# FoodCalorie-Dev-Build

Public workflow-only builder for the private [`FoodCalorie-Dev`](https://github.com/cresent630-glitch/FoodCalorie-Dev) iOS source repository. The `Private iOS build` workflow runs on the GitHub-hosted `xcode-27` macOS runner.

## Test or package a source revision

1. Push your commit to the private source repository. In that checkout, run `git rev-parse HEAD` to get the full 40-character commit SHA.
2. Open [`Private iOS build`](https://github.com/cresent630-glitch/FoodCalorie-Dev-Build/actions/workflows/ios-build.yml), select **Run workflow**, and enter the SHA. The default runs unit tests and reports the result on the source commit. Detailed logs and test bundles stay on the temporary runner. UI tests and a simulator Release build are separate options.
3. To package a device IPA and retain diagnostics, enable `package_ipa`. Check the device build and publication steps, then open [the private releases](https://github.com/cresent630-glitch/FoodCalorie-Dev-Releases/releases) and find `build-<run-id>-<attempt>`, using the run ID from the Actions URL. A delivery rerun publishes under a new attempt number.

The release includes `private-logs.zip` and any available `FoodCalorie-test-results.zip`. A successful device build also includes `FoodCalorie-ipa.zip`, with the unsigned IPA and `build-source.txt` recording its source revision and build tools. Sign the IPA before installing or distributing it. Failed builds can still publish a release containing diagnostics.

## Maintain repository access

Configure `SOURCE_REPO_TOKEN` with **Contents: Read** and **Commit statuses: Read and write** for `FoodCalorie-Dev`. For explicit deliveries, configure `PRIVATE_OUTPUT_TOKEN` with **Contents: Read and write** for `FoodCalorie-Dev-Releases`. Store these as Actions secrets in this builder. The workflow checks that the destination is private and publishes each draft only after its attachments upload.

Restrict maintenance to trusted maintainers and review workflow changes before running private source. Rotate expiring tokens in GitHub Settings and keep private source, logs, and credentials out of this repository.
