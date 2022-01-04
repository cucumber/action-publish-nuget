[![Test](https://github.com/cucumber/action-publish-nuget/actions/workflows/test.yaml/badge.svg)](https://github.com/cucumber/action-publish-nuget/actions/workflows/test.yaml)

# action-publish-nuget

Publishes a .NET package to [NuGet.org](https://nuget.org/)

Needs .NET to be installed first.

## Inputs

* `nuget-api-key`
* `working-directory` (default `.`)

## Example

```yaml
name: Release NuGet

on:
  push:
    branches:
      - "release/*"

jobs:
  publish-nuget:
    name: Publish package to NuGet.org
    runs-on: ubuntu-latest
    environment: Release
    steps:
      - uses: actions/checkout@v2
      - name: Setup .NET
        uses: actions/setup-dotnet@v1
        with:
          dotnet-version: 6.0.x
      - uses: cucumber/action-publish-nuget@v1.0.0
        with:
          nuget-api-key: ${{ secrets.NUGET_API_KEY }}
          working-directory: "dotnet"
```
