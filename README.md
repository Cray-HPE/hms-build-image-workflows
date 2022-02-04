# hms-build-image-workflows

Table of contents
- [hms-build-image-workflows](#hms-build-image-workflows)
  - [Build and release image workflow](#build-and-release-image-workflow)
    - [Workflow Inputs](#workflow-inputs)
    - [Build and release job](#build-and-release-job)
    - [Update PR with comment job](#update-pr-with-comment-job)
  - [Run unit test workflow](#run-unit-test-workflow)
    - [Workflow inputs](#workflow-inputs-1)
  - [Run integration test workflow](#run-integration-test-workflow)
    - [Workflow inputs](#workflow-inputs-2)
  - [Release model](#release-model)


## Build and release image workflow

![](docs/build_and_release_image/overall_workflow_execution.svg)

### Workflow Inputs
| Name                | Data Type | Required Field | Default value             | Description
| ------------------- | --------- | -------------- | ------------------------- | -----------
| `runs-on`           | `string`  | Optional       | `ubuntu-latest`           | The type of machine to run the job on.
| `docker-registry`   | `string`  | Optional       | `artifactory.algol60.net` | Registry to publish container images to.
| `image-name`        | `string`  | Required       |                           | Container image name. For example, cray-firmware-action
| `enable-latest-tag` | `string`  | Optional       | `False`                   | Enable the latest tag for stable builds. Choose from true or false
| `snyk-severity`     | `string`  | Optional       | `high`                    | Only report vulnerabilities of provided level or higher. Choose from: low, medium, high, or critical
| `trivy-enable`      | `string`  | Optional       | `False`                   | Enable or disable the Trivy Vulnerability scanner. Choose from true or false
| `trivy-exit-code`   | `string`  | Optional       | `0`                       | Exit code when vulnerabilities were found
| `trivy-severity`    | `string`  | Optional       | `CRITICAL,HIGH`           | Severities of vulnerabilities to be displayed
| `enable-pr-comment` | `string`  | Optional       | `True`                    | Control whether the update-pr-with-artifacts job runs on PR builds. Choose from true or false

### Build and release job

![](docs/build_and_release_image/build_and_release_job.svg)

### Update PR with comment job

![](docs/build_and_release_image/update_pr_with_artifacts_job.svg)


## Run unit test workflow

![](docs/run_unit_test/run_unit_tests_job.svg)

### Workflow inputs
| Name      | Data Type | Required Field | Default value   | Description
| --------- | --------- | -------------- | --------------- | -----------
| `runs-on` | `string`  | Optional       | `ubuntu-latest` | The type of machine to run the job on.

## Run integration test workflow

![](docs/run_integration_test/run_integration_tests_job.svg)

### Workflow inputs
| Name      | Data Type | Required Field | Default value   | Description
| --------- | --------- | -------------- | --------------- | -----------
| `runs-on` | `string`  | Optional       | `ubuntu-latest` | The type of machine to run the job on.

## Release model

When you make changes you should tag the code branch with an vX.Y.Z semver and move/create the vX tag.

the vX tag (eg v1) is used by the 'invoking' workflows.  The contract is that vX(n) MUST be backwards compatible.  
the vX.Y.Z tag is used to distinguish code changes as a release.