# Security notes for the lab collection

Use disposable systems and credentials. Put real inventory in ignored `inventory.local/`, supply authentication through prompts or Ansible Vault, and avoid committing raw command output or private key material.

The root `ansible.cfg` disables host-key checking as a lab setting. Use verified host keys and enable checking before adapting these examples to other environments. Passwordless sudo examples are demonstrations that need an explicit access decision.

## Scanner findings

The repository includes third-party collections below `ansibleHomeServer/AnsibleHomeServerTesting/collections/ansible_collections/`. Their example strings, documentation, and cryptographic integration-test fixtures trigger Gitleaks rules. Their files and licenses are preserved; findings are not hidden with a blanket allowlist. Review each finding in context and never reuse a fixture key or credential.

## Historical exposure

Passwords committed in older inventory revisions require separate assessment. Removing current assignments does not revoke passwords or erase those revisions. Rotate any affected credential still in use, including any reused elsewhere. A Git history rewrite needs a reviewed plan and coordination with existing clones.

Do not post secret values in issues or pull requests. Keep remediation reports redacted. GitHub's [sensitive-data removal guide](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) describes rotation, history cleanup, and the limits of removing other copies.
