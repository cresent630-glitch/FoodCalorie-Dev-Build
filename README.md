# FoodCalorie-Dev-Build

Public workflow-only builder for the private [`FoodCalorie-Dev`](https://github.com/cresent630-glitch/FoodCalorie-Dev) iOS source repository. The `Private iOS build` workflow runs on the GitHub-hosted `xcode-27` macOS runner.

## Test or package a source revision

`Watch private main` checks the current private `main` revision on a schedule and requests unit tests for revisions without a public builder run. Pull requests can be tested before merge by dispatching their source SHA manually.

1. Push your commit to the private source repository. In that checkout, run `git rev-parse HEAD` to get the full 40-character commit SHA.
2. Open [`Private iOS build`](https://github.com/cresent630-glitch/FoodCalorie-Dev-Build/actions/workflows/ios-build.yml), select **Run workflow**, and enter the SHA. The default runs unit tests and reports the result on the source commit. Detailed logs and test bundles stay on the temporary runner. UI tests and a simulator Release build are separate options.
3. Get the project owner's explicit approval before using storage for a run or rerun. Select `storage_approved` to record that approval, then select only the approved output. `package_ipa` publishes the device package. `publish_diagnostics` retains detailed logs and available test results. Check [the private releases](https://github.com/cresent630-glitch/FoodCalorie-Dev-Releases/releases) for `build-<run-id>-<attempt>`. Prefer reusing an existing delivery for the same source revision.

A successful package includes `FoodCalorie-ipa.zip`, with the unsigned IPA and `build-source.txt` recording its source revision and build tools. Sign the IPA before installing or distributing it. A run without a successful package publishes a release only when diagnostics were requested. Private releases remain available until the owner cleans them up.

## Maintain repository access

Configure `SOURCE_REPO_TOKEN` with **Contents: Read** and **Commit statuses: Read and write** for `FoodCalorie-Dev`. For explicit deliveries, configure `PRIVATE_OUTPUT_TOKEN` with **Contents: Read and write** for `FoodCalorie-Dev-Releases`. Store these as Actions secrets in this builder. The workflow checks that the destination is private and publishes each draft only after its attachments upload.

Restrict maintenance to trusted maintainers and review workflow changes before running private source. Rotate expiring tokens in GitHub Settings and keep private source, logs, and credentials out of this repository.
