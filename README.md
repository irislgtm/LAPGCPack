# LAPGC Modpack

Minecraft 1.12.2 modpack built from this repo via GitHub Actions.

## Installing

1. Go to the [Actions tab](https://github.com/irislgtm/LAPGCPack/actions) and click the latest successful run
2. Under **Artifacts**, download `modpack`
3. Unzip the downloaded archive — inside you'll find `modpack-latest.zip`
4. In PrismLauncher: **Add Instance → Import from ZIP** and select `modpack-latest.zip`

Releases (when tagged) also have the ZIP attached directly with no double-zipping.

## Contributing

The repo tracks **config, groovy scripts, and mod metadata** — not jar files (except WitcheryResurrected, which isn't on CurseForge).

### Adding/removing a mod

Mod metadata lives in `minecraft/mods/.index/` as packwiz `.pw.toml` files:

```toml
name = "Mod Name"
filename = "mod-file-1.0.jar"

[update.curseforge]
file-id = 1234567
```

- **Add a mod**: drop the `.pw.toml` into `.index/` and the jar into `minecraft/mods/`
- **Remove a mod**: delete both the `.pw.toml` and the jar
- **Update a mod**: update the `file-id` (CurseForge) or URL (Modrinth) in the `.pw.toml`

### Changing configs

Edit files under `minecraft/config/` or `minecraft/groovy/` — they're tracked and included in every build.

### Commit & push

```powershell
git add -A
git commit -m "description of changes"
git push
```

The CI will automatically build a fresh ZIP and upload it as an artifact.

### Direct jar tracking

If a mod isn't on CurseForge or Modrinth, force-add the jar so the CI picks it up:

```powershell
git add -f minecraft/mods/mod-name.jar
```

Then create a `.pw.toml` entry with a `[update.direct]` section so `update.py` won't delete it.
