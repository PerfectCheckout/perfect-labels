# Perfect Labels

GitHub action to sync a repo's issue labels with the standard Perfect set.

## Usage

To use this action, create the following file in your GitHub repo:

```
.github/workflows/sync-repo-labels.yml
```

```yml
on: [issues, pull_request]
jobs:
  sync-labels:
    runs-on: ubuntu-latest
    name: Sync repository labels
    steps:
      - uses: PerfectCheckout/perfect-labels@v1
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

:warning: Whenever an issue is opened, the workflow will execute. This overrides all labels in the repository and may result in loss of data if it's run on a repo that isn't owned by Perfect.

You can do this by running the following command from a repo:

```bash
mkdir -p .github/workflows && curl https://raw.githubusercontent.com/PerfectCheckout/perfect-labels/v1/example.yml --output .github/workflows/sync-repo-labels.yml
```

## Labels

You can find the current labels in [`./labels.json`](labels.json). Edit this file to make changes to Perfect's suite of labels.

### Changing a label name

When you want to change a label's name, it's very important to add the _old_ label name to the list of aliases for that label. This will ensure that the label is renamed rather than being removed then created. Failing to do this will result in loss of data.

  1. Copy the value of the `name` property and add a new entry in that label's `aliases` array
  2. Change the `name` property of the label to your new value

### Changing a label description

Change the `description` property for the label you wish to update.

### Changing a label colour

Add the new colour value to the `colors` object. Change the `color` property for the label you wish to update.

## Development

Run `npm install` first.

Work should be based on the `trunk` branch, with changes PR'ed in.

If your changes are not breaking, merge them into the `v1` branch, and they'll be picked up by every repo running `v1` automatically.

If your changes ARE breaking, then you should create a new `v2` branch based on trunk and update your chosen repo to use the new workflow.
