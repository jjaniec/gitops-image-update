# GitOps: Update Image Tag

This GitHub Action updates the Image Tag in a GitOps repository. It's designed to streamline the process of modifying image tags in your infrastructure-as-code (IaC) setups.

## Use Case

-  ✅ You have a GitOps repository that contains the IaC for your infrastructure.
-  ✅ You have a CI/CD pipeline that builds and pushes Docker images to a registry. 
-  **This is what this action does →** You want to update the image tag in the GitOps repository whenever a new image is pushed to the registry. 

## Mandatory Inputs

* `REPOSITORY_NAME`: Owner and repository name of the GitOps repository.
* `VALUES_FILE_PATH`: Path to the values file in the GitOps repository (e.g., api-something/values.yaml).
* `VALUE_NAME`: Name of the value in the values file (e.g., `frontendImageTag`).
* `TAG`: Name of the Image Tag (e.g., `v1.0.0` or `e0f9a8b`).

## Optional Inputs

* `ACCESS_TOKEN`: (Personal) Access Token for the GitOps repository. Defaults to `${{ github.token }}`. A personal access token is required if the GitOps repository is private or if the action is triggered by a workflow in another repository.
* `BRANCH`: Branch of the GitOps repository. Defaults to `main`.
* `USERNAME`: Username for the GitOps repository. Defaults to `${{ github.actor }}`.

## Usage

To use this action, add a step to your github workflow file. Like this example:

```yaml
- name: GitOps - Update Image Tag
  uses: jjaniec/gitops-image-update@v1
  with:
    API_NAME: api-something
    ENV_NAME: dev
    REPOSITORY_NAME: 'jjaniec/gitops-repository'
    ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
    BRANCH: "master"
    VALUES_FILE_PATH: 'api-something/values.dev.yaml'
    VALUE_NAME: 'tag'
    TAG: '${{ github.sha }}'

```
