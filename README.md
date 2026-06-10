# LAPGC Modpack

Minecraft 1.12.2 modpack. Builds are produced automatically by GitHub Actions.

## Installing (players)

1. Go to the [Actions tab](https://github.com/irislgtm/LAPGCPack/actions)
2. Click the latest successful run, scroll to **Artifacts**, download `modpack`
3. Unzip once — inside is `modpack-latest.zip`
4. PrismLauncher: **Add Instance → Import from ZIP** → select `modpack-latest.zip`

Releases (tagged versions) have the ZIP as a direct download with no extra nesting.

## Contributing

You need a local git clone of this repo. The CI output is a PrismLauncher instance — it's **not** a git repo and can't be pushed from.

### Setup

```powershell
git clone https://github.com/irislgtm/LAPGCPack
cd LAPGCPack
```

### Adding / removing a mod

Mod metadata lives in `minecraft/mods/.index/` as packwiz `.pw.toml` files:

```toml
name = "Mod Name"
filename = "mod-file-1.0.jar"

[update.curseforge]
file-id = 1234567
```

- **Add**: create a `.pw.toml` in `.index/` with the CurseForge file-id or Modrinth URL, then drop the jar in `minecraft/mods/`
- **Remove**: delete both the `.pw.toml` and the jar
- **Update**: change the `file-id` / URL in the `.pw.toml`

### Changing configs / scripts

Edit files under `minecraft/config/` and `minecraft/groovy/`. Everything there is tracked and included in every CI build.

### Mods without CurseForge/Modrinth

If a mod isn't on those platforms, force-add the jar so the CI bundles it:

```powershell
git add -f minecraft/mods/mod-name.jar
```

Add a `.pw.toml` entry so `update.py` won't delete it on the next CI run.

### Testing changes locally

Copy your changes into your PrismLauncher instance to test:

```powershell
# from the repo root
Copy-Item -Recurse minecraft/config "C:\Users\...\instances\YourInstance\minecraft\config"
Copy-Item -Recurse minecraft/mods "C:\Users\...\instances\YourInstance\minecraft\mods"
```

Or symlink the instance's `minecraft` folder to the repo for real-time testing.

### Commit & push

```powershell
git add -A
git commit -m "what changed"
git push
```

The CI builds a fresh ZIP automatically.
