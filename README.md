# Push Docker Image to Google Artifact Registry (GAR) using GitHub Actions

This GitHub Action builds and pushes a Docker image to Google Artifact Registry.

## Inputs

| Name                | Description                                      | Required |
|---------------------|--------------------------------------------------|----------|
| `gcloud_service_key`| The GCP service account key in base64 encoded JSON | true     |
| `project_id`        | The GCP project ID                               | true     |
| `registry`          | The GAR registry location                        | true     |
| `repository`        | The GAR repository name                          | true     |
| `image_name`        | The name of the Docker image                     | true     |
| `image_tags`        | Comma-separated list of tags for the Docker image| true     |
| `dockerfile`        | Path to the Dockerfile                           | true     |
| `build_args`        | Build arguments for Docker                       | false    |

## Usage

```yaml
name: Push Docker Image to GAR

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Push Docker img to GAR
        uses: ./.github/actions/push-docker-gar
        with:
          gcloud_service_key: ${{ secrets.GCLOUD_SERVICE_KEY }}
          project_id: ${{ secrets.GCP_PROJECT_ID }}
          registry: ${{ secrets.GAR_REGISTRY }}
          repository: ${{ secrets.GAR_REPOSITORY }}
          image_name: 'your-image-name'
          image_tags: 'latest,stable'
          dockerfile: './Dockerfile'
          build_args: 'ARG1=value1,ARG2=value2'

