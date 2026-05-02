# Custom Repository for Patch 7.5

This fork is prepared for FFXIV Patch 7.5 / Dalamud API 15.

Relevant bump:

- `Echoglossian.csproj` uses `Dalamud.NET.Sdk/15.0.0`.
- `DalamudPackager` is pinned to `15.0.0`.
- `TargetFramework` is `net10.0-windows`.
- The default `VersionSeries` is `75`, so custom builds sort above earlier 7.x builds.

## Publish through GitHub Actions

1. Push this branch to your fork:

   ```powershell
   git push -u origin codex/patch-7-5
   ```

2. In GitHub, open `wevtimoteo/Echoglossian` > `Settings` > `Pages`.

3. Set `Build and deployment` > `Source` to `GitHub Actions`.

4. Open `Actions` > `Publish Custom Dalamud Repository`.

5. Click `Run workflow` and run it from `codex/patch-7-5`.

6. After the workflow finishes, your custom repository URL should be:

   ```text
   https://wevtimoteo.github.io/Echoglossian/pluginmaster.json
   ```

The workflow publishes both:

- `https://wevtimoteo.github.io/Echoglossian/pluginmaster.json`
- `https://wevtimoteo.github.io/Echoglossian/latest.zip`

## Add it in Dalamud

1. In game, run `/xlsettings`.

2. Open the `Experimental` tab.

3. Under `Custom Plugin Repositories`, add:

   ```text
   https://wevtimoteo.github.io/Echoglossian/pluginmaster.json
   ```

4. Click the plus button, then save.

5. Open `/xlplugins`, search for `Echoglossian`, and install or update it.

If you already have the official Echoglossian installed, uninstalling it first can make it clearer that the install is coming from your custom repository.

## Local build option

Local builds require .NET SDK 10.

```powershell
$env:DALAMUD_HOME = "$PWD\.dalamud\dev"
dotnet restore Echoglossian.sln -r win-x64
dotnet build Echoglossian.sln --configuration Release -p:VersionSeries=75
```

If `.dalamud\dev` does not exist yet, download the current staging Dalamud build first:

```powershell
New-Item -ItemType Directory -Force .dalamud | Out-Null
Invoke-WebRequest -Uri https://goatcorp.github.io/dalamud-distrib/stg/latest.zip -OutFile .dalamud\latest.zip
Expand-Archive -Force .dalamud\latest.zip .dalamud\dev
```

Depois do build, procure pelo `latest.zip` gerado pelo `DalamudPackager`. Para usar como custom repository, esse zip precisa estar hospedado em uma URL HTTP publica e o `pluginmaster.json` precisa apontar para essa URL nos campos `DownloadLinkInstall` e `DownloadLinkUpdate`.

## Immediate local repository

For a quick local smoke test, create `local-repo\pluginmaster.json`, copy `latest.zip` there, and serve it on localhost:

```powershell
python -m http.server 8765 --bind 127.0.0.1 --directory local-repo
```

Then add this URL in Dalamud:

```text
http://127.0.0.1:8765/pluginmaster.json
```
