# Ansible Vault Demo

This repository contains a demonstration of Ansible Vault features for managing secrets and sensitive data in Ansible playbooks.

## Prerequisites

- Ansible installed (version 2.9 or higher)
- Basic understanding of YAML and Ansible playbooks

## Directory Structure

```plaintext
ansible-vault-demo/
├── group_vars/
│   └── all/
│       ├── vault.yml (encrypted)
│       └── vars.yml
├── inventory.ini
└── playbook.yml
```

## Setup Instructions

1. Create the project directory:

```bash
mkdir ansible-vault-demo
cd ansible-vault-demo
```

2. Create the required directory structure:

```bash
mkdir -p group_vars/all
```

3. Create an inventory file (`inventory.ini`):

```ini
[local]
localhost ansible_connection=local
```

## Step-by-Step Demo

### 1. Creating an Encrypted File

Create an encrypted file to store sensitive data:

```bash
ansible-vault create group_vars/all/vault.yml
```

When the editor opens, add these contents:

```yaml
vault_api_key: "super-secret-api-key"
vault_db_password: "database-password-123"
vault_secret_token: "secret-token-456"
```

### 2. Creating a Variables File

Create `group_vars/all/vars.yml` to reference the encrypted variables:

```yaml
# Reference encrypted variables
api_key: "{{ vault_api_key }}"
db_password: "{{ vault_db_password }}"
secret_token: "{{ vault_secret_token }}"
```

### 3. Create a Demo Playbook

Create `playbook.yml`:

```yaml
---
- hosts: local
  gather_facts: no
  
  tasks:
    - name: Display encrypted values (for demo only!)
      debug:
        msg: 
          - "API Key: {{ api_key }}"
          - "DB Password: {{ db_password }}"
          - "Secret Token: {{ vault_secret_token }}"
```

## Usage Examples

### Basic Vault Operations

1. Run playbook with password prompt:
```bash
ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass
```

2. Create and use a password file (demo only):
```bash
echo "demo-password" > vault-pass.txt
ansible-playbook -i inventory.ini playbook.yml --vault-password-file vault-pass.txt
```

3. View encrypted file:
```bash
ansible-vault view group_vars/all/vault.yml
```

4. Edit encrypted file:
```bash
ansible-vault edit group_vars/all/vault.yml
```

5. Encrypt an existing file:
```bash
echo "new_secret: value" > plain.yml
ansible-vault encrypt plain.yml
```

6. Decrypt a file:
```bash
ansible-vault decrypt plain.yml
```

7. Change vault password:
```bash
ansible-vault rekey group_vars/all/vault.yml
```

### Advanced: Multiple Vault Passwords

1. Create environment-specific vault files:
```bash
# Create dev vault
ansible-vault create --vault-id dev@prompt group_vars/all/dev-vault.yml

# Create prod vault
ansible-vault create --vault-id prod@prompt group_vars/all/prod-vault.yml
```

2. Run playbook with multiple vault passwords:
```bash
ansible-playbook -i inventory.ini playbook.yml --vault-id dev@prompt --vault-id prod@prompt
```

## Cleanup

Remove demo files and directories:

```bash
# Remove password file
rm vault-pass.txt

# Remove entire demo directory
cd ..
rm -rf ansible-vault-demo
```

## Best Practices

1. Never commit vault passwords or unencrypted sensitive data
2. Use different vault passwords for different environments
3. Store vault passwords securely (not in version control)
4. Regularly rotate vault passwords
5. Only encrypt necessary values, not entire files
6. Use descriptive names for vault files

## Common Issues and Solutions

1. **Error: Vault password file not found**
   - Ensure the vault password file exists and has correct permissions
   - Use `--ask-vault-pass` instead for interactive password entry

2. **Error: Vault decryption failed**
   - Verify you're using the correct vault password
   - Check if the file is actually encrypted with ansible-vault

3. **Error: Multiple vault passwords required**
   - Use `--vault-id` option for each required password
   - Ensure all referenced vault files are accessible

## Additional Resources

- [Ansible Vault Documentation](https://docs.ansible.com/ansible/latest/user_guide/vault.html)
- [Ansible Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)
- [Ansible Security](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html#security)

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is licensed under the MIT License - see the LICENSE file for details.
