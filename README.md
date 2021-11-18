[![Test](https://github.com/cucumber/action-publish-nuget/actions/workflows/test.yaml/badge.svg)](https://github.com/cucumber/action-publish-nuget/actions/workflows/test.yaml)

# action-publish-nuget

Publishes a .NET package to [NuGet.org](https://nuget.org/)

Needs .NET to be installed first.

## Inputs

* `nuget-api-key`
* `working-directory` (default `.`)

## Example

```yaml
name: Publish

on:
  push:
    branches:
      - "release/*"

jobs:
  publish-dotnet-nuget:
    name: Publish package to NuGet.org
    runs-on: ubuntu-latest
    environment: Release
    steps:
      - uses: actions/checkout@v2
      - name: Setup .NET
        uses: actions/setup-dotnet@v1
        with:
          dotnet-version: 6.0.x
      - name: Test the action
        uses: cucumber/action-publish-nuget@v1.0.0
        with:
          nuget-api-key: ${{ secrets.NUGET_API_KEY }}
          working-directory: "java"
```
