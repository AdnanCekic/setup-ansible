# setup-ansible GitHub Action

This GitHub Action installs Ansible on your GitHub Actions runner.

## Usage

```yaml
- uses: AdnanCekic/setup-ansible@v1
    with:
        version: '2.19.3'  # optional, defaults to latest
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
            - uses: actions/checkout@v3
            
            - name: Install Ansible
                uses: AdnanCekic/setup-ansible@v1
                with:
                    version: '2.19.3'
            
            - name: Run playbook
                run: ansible-playbook playbook.yml
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | Version of Ansible to install | No | Latest version |

## License

MIT License

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.