# setup-ansible GitHub Action

This GitHub Action installs Ansible on your GitHub Actions runner.

## Usage

```yaml
- uses: AdnanCekic/setup-ansible@v1
  with:
    version: '2.20.2'  # required
```

## Example Workflow

```yaml
name: Ansible Playbook

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install Ansible
        uses: AdnanCekic/setup-ansible@v1
        with:
          version: '2.20.2'

      - name: Run playbook
        run: ansible-playbook playbook.yml
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Ansible Core version to install (e.g. "2.20.2") | Yes | - |

## Features

- ✅ Isolated virtualenv installation (no system pollution)
- ✅ Smart caching (skips reinstall if version already cached)
- ✅ Python 3.12 with latest actions/setup-python@v6
- ✅ Fast subsequent runs with actions/cache@v6

## License

MIT License

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
