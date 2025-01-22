# Dekode Public GitHub Actions

This repository contains a collection of GitHub Actions, intended to be used in other repositories. Some of them are reusable and can be called directly from a project, while others function as templates for more specific needs.

## Using reusable workflows

To use one of the reusable workflows, call it in your project using the `uses` keyword. For example; For example, to use the `deploy` workflow, add the following to your `.github/workflows/main.yml` file:

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout source
        uses: actions/checkout@v2
        
  remote:
    uses: dekodeinteraktiv/github-actions/.github/workflows/deploy
    with:
      INPUT_VARIABLE: 'value'
    secrets:
      SECRET_NAME: 'value'
```

Note that you can pass `secrets: inherit` to forward all secrets, but unless they fit the workflow expectations, it is better to not over-share secrets, and instead only pass the expected ones.

## Adding a new workflow

When considering adding a new workflow, please be mindful that you've considered its reusability, and that it is generic without any direct individual project tie-ins.

To add a new workflow, create a new file in the `.github/workflows` directory, and add the workflow to it. Make sure the workflow is set to trigger on `workflow_call`, no actions with different triggers should be added to this repository.
[See the GitHub documentation on creating reusable workflows for more information](https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow).

The workflow file should have a descriptive file-name, and the workflow it self should have a name to identify it when used outside of this repository.

## Documenting workflows

To maintain a clean workflow directory, each workflow should be documented with a single file in the [`./workflows` directory](workflows/), with the same file-name as the workflow for easy identification.

Workflow documentation should, as a bare minimum, have a quick description of what the workflow accomplishes, and a list of inputs and outputs. For more complex workflows, it is recommended to add a more detailed description of the workflow, and how to use it.