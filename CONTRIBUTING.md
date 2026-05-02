# Contributing to Uriangenio

Thanks for helping with Uriangenio.

Uriangenio is a fork of [lokinmodar/Echoglossian](https://github.com/lokinmodar/Echoglossian). Please keep that relationship clear in docs, releases, and discussions. The original author and upstream contributors deserve visible credit for the project this fork is based on.

## Project Scope

This fork is focused on keeping a Patch 7.5 / Dalamud API 15 compatible build available under a separate plugin identity.

Good contribution areas include:

- Compatibility fixes for current Dalamud API changes.
- Build, packaging, and custom repository publishing improvements.
- Runtime fixes that affect Uriangenio users.
- Documentation that makes fork status, installation, or maintenance clearer.
- Small safety fixes that avoid leaking credentials, API keys, or local paths.

Changes that are better for upstream first:

- Broad feature work unrelated to Patch 7.5 compatibility.
- Large refactors that make it harder to compare with Echoglossian.
- Branding changes that blur the distinction between Uriangenio and Echoglossian.

## Branch Policy

This fork is maintained directly from `main`.

For small maintainer changes, commit directly to `main`. For external contributions, open a pull request targeting `main`.

Keep branches short lived and delete them after merge.

## Prerequisites

- Windows.
- .NET SDK 10.
- A local Dalamud staging/dev build.
- GitHub CLI if you are publishing releases or inspecting Actions.

The project uses `global.json` to select the .NET SDK. If restore fails with an SDK version error, install the .NET 10 SDK or update your SDK installation.

## Local Setup

Download the current Dalamud staging build into `.dalamud/dev`:

```powershell
New-Item -ItemType Directory -Force .dalamud | Out-Null
Invoke-WebRequest -Uri https://goatcorp.github.io/dalamud-distrib/stg/latest.zip -OutFile .dalamud\latest.zip
Expand-Archive -Force .dalamud\latest.zip .dalamud\dev
```

Set `DALAMUD_HOME` for the current shell:

```powershell
$env:DALAMUD_HOME = "$PWD\.dalamud\dev"
```

Restore and build:

```powershell
dotnet restore Echoglossian.sln -r win-x64
dotnet build Echoglossian.sln --configuration Release -p:VersionSeries=75
```

Run the same test command used by CI:

```powershell
dotnet test Echoglossian.sln --configuration Release --no-build --verbosity normal
```

## Packaging

The release build produces a Dalamud package under:

```text
bin\x64\Release\win-x64\Uriangenio\latest.zip
```

The packaged manifest should be:

```text
bin\x64\Release\win-x64\Uriangenio\Uriangenio.json
```

Before publishing, verify that the plugin identity remains:

- `Name`: `Uriangenio`
- `InternalName`: `Uriangenio`
- `Author`: `wevtimoteo`
- `RepoUrl`: `https://github.com/wevtimoteo/Uriangenio`

## Custom Repository Publishing

The release-based custom repository URL is:

```text
https://github.com/wevtimoteo/Uriangenio/releases/latest/download/pluginmaster.json
```

Release assets must include:

- `pluginmaster.json`
- `latest.zip`

`pluginmaster.json` must point `DownloadLinkInstall`, `DownloadLinkUpdate`, and `DownloadLinkTesting` to a reachable `latest.zip`.

## Local Custom Repository Testing

For a local smoke test, serve a generated local repository:

```powershell
python -m http.server 8765 --bind 127.0.0.1 --directory local-repo
```

Then add this URL in Dalamud as a custom plugin repository:

```text
http://127.0.0.1:8765/pluginmaster.json
```

Use `Custom Plugin Repositories`, not `Dev Plugin Locations`, for this URL.

## Security

Do not commit:

- API keys or translation provider credentials.
- Personal Dalamud configuration.
- Local logs.
- `.dalamud`, `.dotnet_home`, `local-repo`, `bin`, or `obj` contents.
- GitHub tokens, PATs, or release upload credentials.

Before committing, run:

```powershell
git status -sb
git diff --check
git diff --cached
```

Review staged files for secrets and machine-specific paths.

## Pull Request Checklist

- The change is scoped to this fork's maintenance goals.
- Original Echoglossian credit remains intact.
- The plugin still builds with .NET 10 and Dalamud API 15.
- Public docs clearly refer to Uriangenio as a fork.
- No local artifacts or secrets are included.

## License and Attribution

Uriangenio inherits the licensing and attribution obligations of Echoglossian. Keep original notices, upstream links, and contributor credits visible unless there is a clear legal or maintenance reason to adjust them.
