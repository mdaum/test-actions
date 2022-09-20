# Testing github actions before making PRs elsewhere

Current action lets you publish docker image

## Inputs

This action requires uses the following inputs:

| Name               | Type     | Description                                                                        |
|--------------------|----------|------------------------------------------------------------------------------------|
| `package-name`     | String   | Name that the image should be published as to Docker Hub as                        |
| `docker-username`  | String   | Username for the docker account to publish under                                   |
| `docker-password`  | String   | Password for the docker account to publish under                                   |
| `push-to-registry` | String   | Determine if the built image should be pushed to registry (Default is 'false')     |

The docker username and password will likely be passed by `secrets`. You must ensure your repo has access to these secret variables

## Example Usage:

```yaml
jobs:
  ...

  publish-image:
    runs-on: ubuntu-latest
    if: env.publish == 'true' # Only publish when releasing a new version to main
    steps:
      - uses: actions/checkout@v3
      - id: publish-image
        uses: jupiterone/publish-integration-image-action@v1
        with:
          package-name: 'jupiterone/graph-kubernetes'
          docker-username: ${{ secrets.DOCKERHUB_USERNAME }}
          docker-password: ${{ secrets.DOCKERHUB_TOKEN }}
          push-to-registry: 'true'
```

