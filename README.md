# setup-ansible

Installs a pinned `ansible-core` into an isolated virtualenv with [uv](https://docs.astral.sh/uv/). Works on GitHub-hosted and self-hosted runners, including self-hosted Ubuntu runners without sudo whose system Python lacks `venv`, `ensurepip` and `pip`.

## Usage

```yaml
- uses: AdnanCekic/setup-ansible@v2
  with:
    version: "2.20.1"
```

With extra Python packages in the same virtualenv:

```yaml
- uses: AdnanCekic/setup-ansible@v2
  with:
    version: "2.20.1"
    python-version: "3.13"
    extra-packages: "pywinrm jmespath"
```

After the step, `ansible`, `ansible-playbook`, `ansible-galaxy`, `python` and `pip` from the virtualenv are on `PATH`, and `VIRTUAL_ENV` points to it. Later `pip install` or `uv pip install` calls go into the same virtualenv.

## Inputs

| Input | Description | Default |
|---|---|---|
| `version` | Exact `ansible-core` version, required | |
| `python-version` | Python version for the virtualenv; uv downloads it if the runner lacks it | `3.12` |
| `extra-packages` | Extra pip packages, space separated; the `ansible-core` pin constrains them | `""` |

## Outputs

| Output | Description |
|---|---|
| `ansible-version` | Installed `ansible-core` version |
| `venv` | Path to the virtualenv |

## How it works

1. Installs uv with `astral-sh/setup-uv`, pinned to a commit.
2. Creates a fresh virtualenv under `$RUNNER_TEMP` with `uv venv --seed`. uv builds the virtualenv itself, so the runner needs neither sudo nor Python's `venv` module.
3. Installs `ansible-core==<version>` plus the extra packages in one resolve, then fails if any other `ansible-core` version ended up installed.

There is no Actions cache: uv installs `ansible-core` in a few seconds, and on self-hosted runners uv's own cache in the home directory persists between jobs.

Linux and macOS runners only. Ansible does not run on Windows as a control node.

## Upgrading from v1

- The virtualenv no longer lives in `.venv` inside the workspace, and the Actions cache is gone.
- `extra-packages` replaces a separate `pip install` step. That step still works, because `pip` from the virtualenv is on `PATH`.
- `version` must be an exact version such as `2.20.1`.

## License

MIT
