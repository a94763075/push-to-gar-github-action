<img width="867" alt="截圖 2024-07-16 下午6 02 37" src="https://github.com/user-attachments/assets/a61a96fd-d273-486c-b29d-2b246f3e4f79"># Push Docker Image to Google Artifact Registry (GAR) using GitHub Actions

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
        uses: a94763075/push-to-gar-github-action@v0.1.0
        with:
          gcloud_service_key: ${{ secrets.GCLOUD_SERVICE_KEY }}
          project_id: ${{ secrets.GCP_PROJECT_ID }}
          registry: ${{ secrets.GAR_REGISTRY }}
          repository: ${{ secrets.GAR_REPOSITORY }}
          image_name: 'your-image-name'
          image_tags: 'latest,stable'
          dockerfile: './Dockerfile'
          build_args: 'ARG1=value1,ARG2=value2'


## Find

You can find project_id, registry, repository, image_name on Artifact Registry that you created
<img width="867" alt="截圖 2024-07-16 下午6 02 37" src="https://github.com/user-attachments/assets/818d5781-f97d-43d1-8d73-151a85460b4c">
