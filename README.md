# LAPGC Modpack

Minecraft 1.12.2 modpack. Builds are produced automatically by GitHub Actions.

## Installing (players)

1. Go to the [Actions tab](https://github.com/irislgtm/LAPGCPack/actions)
2. Click the latest successful run, scroll to **Artifacts**, download `modpack`
3. Unzip once — inside is `modpack-latest.zip`
4. PrismLauncher: **Add Instance → Import from ZIP** → select `modpack-latest.zip`

Releases (tagged versions) have the ZIP as a direct download with no extra nesting.

## Contributing

Clone the repo into a fresh folder inside your PrismLauncher instances directory, then download the mods:

```powershell
cd C:\Users\YOUR_USER\AppData\Roaming\PrismLauncher\instances
git clone https://github.com/irislgtm/LAPGCPack
cd LAPGCPack
python update.py
```

This downloads all mod jars from CurseForge/Modrinth. The repo only tracks configs and mod metadata. After `update.py` finishes, `LAPGCPack/` appears in your launcher and any change you make is tracked by git.

Don't clone into an existing instance folder — start from a clean directory.

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

Force-add the jar so the CI bundles it:

```powershell
git add -f minecraft/mods/mod-name.jar
```

Add a `.pw.toml` entry so `update.py` won't delete it on the next CI run.

### Commit & push

```powershell
git add -A
git commit -m "what changed"
git push
```

The CI builds a fresh ZIP automatically.
