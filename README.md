# setup-ansible GitHub Action

Install Ansible on GitHub Actions runners — works on both **GitHub-hosted** and **self-hosted** runners.

## Usage

```yaml
- uses: AdnanCekic/setup-ansible@v1
  with:
    version: '2.20.1'  # required
```

### Self-hosted runners

If `actions/setup-python` fails (no pre-cached Python), the action automatically
falls back to installing Python 3 from the system package manager (apt, dnf, yum, apk).

You can also override the Python version:

```yaml
- uses: AdnanCekic/setup-ansible@v1
  with:
    version: '2.20.1'
    python-version: '3.11'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Ansible Core version to install | Yes | - |
| `python-version` | Python version for `setup-python` | No | `3.12` |

## Features

- Isolated virtualenv installation (no system pollution)
- Smart caching (skips reinstall if version already cached)
- Self-hosted runner support (auto-installs Python if needed)
- Fast subsequent runs with actions/cache

## License

MIT License
