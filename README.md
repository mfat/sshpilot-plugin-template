# Example sshPilot plugin (template)

A minimal, working [sshPilot](https://github.com/mfat/sshpilot) plugin you can
fork to build your own. It registers an "Example" protocol that runs a
configurable command in the terminal — replace the backend in `__init__.py` with
your real protocol or UI page.

**Use this template:** click *"Use this template"* above, or copy this repo.

See the [plugin developer guide](https://github.com/mfat/sshpilot/blob/main/docs/plugins/writing-plugins.md).

## Layout

```
.
├── plugin.json                 # manifest (id, name, api_version, permissions)
├── __init__.py                 # exposes `class Plugin(SshPilotPlugin)`
├── tests/test_plugin.py        # unit tests (no GTK needed)
└── .github/workflows/test.yml  # CI: pytest against the published sshpilot API
```

## Make it your own

1. Change `id`, `name`, and `permissions` in `plugin.json` (the `id` is your
   directory name and keyring/settings namespace).
2. Rewrite `__init__.py` — keep `class Plugin(SshPilotPlugin)`; register a
   protocol (`ctx.register_protocol(...)`) and/or a UI page (`ctx.ui.register_page(...)`).
3. Update `tests/`.

## Install it (to try it)

```sh
cp -r . ~/.local/share/sshpilot/plugins/example-plugin
```

…or use **Preferences ▸ Plugins ▸ Install plugin…** (folder or zip), enable it,
and restart sshPilot.

## Test it

```sh
pip install pytest
pip install "sshpilot @ git+https://github.com/mfat/sshpilot" --no-deps
pytest -ra
```

## Publish it

Create a GitHub **release** with `your-plugin.zip` + `your-plugin.zip.sha256`,
then PR an entry into
[mfat/sshpilot-plugins](https://github.com/mfat/sshpilot-plugins). Only plugins
meeting the [CONTRIBUTING bar](https://github.com/mfat/sshpilot/blob/main/CONTRIBUTING.md#plugins)
belong in sshPilot core; everything else lives in your repo.
