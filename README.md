[![Test](https://github.com/cucumber/action-publish-nuget/actions/workflows/test.yaml/badge.svg)](https://github.com/cucumber/action-publish-nuget/actions/workflows/test.yaml)

# action-publish-nuget

Publishes a .NET package to [NuGet.org](https://nuget.org/) using [trusted publishing](https://learn.microsoft.com/en-us/nuget/nuget-org/trusted-publishing).

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
      - name: NuGet login (OIDC → temp API key)
        uses: NuGet/login@v1.2.0
        id: login
        with:
          user: ${{ secrets.NUGET_USER }}
      - uses: cucumber/action-publish-nuget@v2.0.0
        with:
          nuget-api-key: ${{ steps.login.outputs.NUGET_API_KEY }}
          working-directory: "dotnet"
```
