Sure, here's a possible README for the Informasjonsforvaltning/workflows repository:

# Informasjonsforvaltning Workflows

This repository contains a collection of GitHub workflows intended for use in Informasjonsforvaltning projects. <br />
The workflows are defined using [GitHub Actions](https://github.com/features/actions) and are intended to automate common tasks such as building, testing, and deploying code.

## Usage

To use the workflows in this repository, you can call them directly from your own workflow:

```Code
jobs:
  build-and-deploy:
    name: Call reusable workflow
    uses: Informasjonsforvaltning/workflows/.github/workflows/build-deploy.yaml@main
    with:
      app_name: example
      environment: example-env
      cluster: example-cluster
    secrets:
      GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Required inputs & secrets
Most workflows requires three inputs passed from the calling workflow, necessary for pod naming, image tagging, helm setup, Slack notifications, etc.:
- `app_name`: Name of the application. 
- `cluster`: Name of the cluster where the application is deployed.
- `environment`: Kubernetes namespace

Most workflows also requires four secrets passed from the calling workflow:
- `GH_TOKEN`: GITHUB_TOKEN, for access
- `GCP_SA_DIGDIR_FDK_GCR_KEY`: For pushing to the container registry
- `DIGDIR_FDK_AUTODEPLOY`: For deploying to the cluster
- `SLACK_WEBHOOK_URL`: For sending status messages to Slack

In order to make the workflow work properly, you need to provide all required inputs and secrets for that specific workflow.

## List of workflows:

- `build-deploy.yaml`: Builds a docker image with a given Dockerfile, pushes it to our Google Cloud registry, and deploys the image to Google Cloud.
- `build-deploy-maven.yaml`: Specific for Java/Kotlin applications. Runs tests with coverage/maven.
- `build-deploy-nox.yaml`: Specific for Python applications. Runs tests with coverage/(or nox if applicable).
- `build-push.yaml`: Builds a docker image with a given Dockerfile and pushes it to our Google Cloud registry.
- `codeql.yaml`: Runs a [CodeQL-scan](https://docs.github.com/en/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/about-code-scanning-with-codeql) based on language set as input.
- `coverage-go.yaml`: Runs a [Codecov action](https://github.com/codecov/codecov-action) specific for Go-code.
- `coverage-node.yaml`: Runs a [Codecov action](https://github.com/codecov/codecov-action) specific for npm.
- `coverage-nox.yaml`: Runs a [Codecov action](https://github.com/codecov/codecov-action) specific for nox.
- `deploy.yaml`: Deploys an image to Google Cloud.
- `deploy-cloud-function.yaml`: Deploys a [Cloud Function](https://cloud.google.com/functions/docs) to Google Cloud.
- `grafana-dashboard-deploy.yaml`: Deploys Grafana Dashboards to our production Grafana instance.
- `grafana-dashboard-preview.yaml`: Creates Grafana dashboard previews in our development Grafana instance.
- `kustomize-deploy.yaml`: Deploys an image with kustomize (requires kustomize config).
- `lint-node-npm.yaml`: Runs lint on npm/node projects.
- `release-draft.yaml`: Drafts release notes.
- `release-poetry.yaml`: Publish new python package to PyPi.
- `safety-nox.yaml`: Specific for Python/Nox applications, intended for pull requests. Runs a safety scan and comments results on PR.
- `test-nox.yaml`: Specific for Python/Nox applications, run tests.
- `test-pypi.yaml`: Test and publish python package to testPyPi.
- `test-rust.yaml`: Specific for Rust applications, run tests w/coverage.

## Contributing

Contributions to this repository are welcome. If you have a new workflow to contribute or an improvement to an existing workflow, please open a pull request.

## License

The workflows in this repository are licensed under the [Apache License, version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
