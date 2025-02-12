# Ansible Vault Lab Assignment

## Overview
In this lab, you will create your own repository demonstrating your understanding of Ansible Vault for managing secrets and sensitive data in Ansible playbooks. You'll build the project step by step and submit your repository link for grading.

## Assignment Requirements

### Prerequisites
- GitHub account
- Ansible installed (version 2.9 or higher)
- Git installed locally
- Basic understanding of YAML and Ansible playbooks

### Assignment Steps

#### 1. Repository Setup (10 points)
1. Create a new GitHub repository named `ansible-vault-lab`
2. Clone your repository locally
3. Create the following directory structure:

```plaintext
ansible-vault-lab/
├── group_vars/
│   └── all/
│       ├── vault.yml (encrypted)
│       └── vars.yml
├── inventory/
│   └── production.ini
├── playbooks/
│   ├── create_user.yml
│   └── configure_service.yml
├── README.md
└── requirements.txt
```

#### 2. Implement Basic Vault Operations (30 points)

1. Create an encrypted `vault.yml` with the following structure:
```yaml
vault_user_password: "secure_password123"
vault_api_key: "api_key_123456"
vault_db_credentials:
  username: "db_admin"
  password: "db_pass_123"
```

2. Create `vars.yml` referencing the vault variables:
```yaml
# Add your reference variables here
```

3. Create two playbooks that use these encrypted values:
   - `create_user.yml`: Creates a user with the encrypted password
   - `configure_service.yml`: Sets up a service using the API key

#### 3. Multiple Environment Setup (30 points)

1. Create separate vault files for development and production:
   - `group_vars/all/dev_vault.yml`
   - `group_vars/all/prod_vault.yml`

2. Implement different values for each environment

3. Document how to run playbooks with different environment credentials

#### 4. Documentation (30 points)

Update the README.md with:
1. Setup instructions
2. Usage examples
3. Description of each playbook
4. Instructions for vault password management
5. Examples of running playbooks with different environment credentials

### Required Demonstrations

Your repository must show examples of:
1. Creating encrypted files
2. Using encrypted values in playbooks
3. Multiple environment support
4. Proper password management
5. `.gitignore` configuration

## Submission Instructions

1. Ensure your repository includes:
   - All required files and directories
   - Comprehensive README.md
   - `.gitignore` with appropriate entries
   - Example playbooks
   - Encrypted vault files (remember not to commit actual secrets!)

2. Submit your assignment:
   - Submit the GitHub repository URL
   - Ensure the repository is public
   - Include any test user/password in your submission (not in the repo!)

## Grading Criteria

- Repository Structure (10%)
- Vault Implementation (30%)
- Multiple Environment Setup (30%)
- Documentation Quality (20%)
- Code Quality and Best Practices (10%)

## Testing Your Submission

Before submitting, verify:
1. Clone your repository to a new directory
2. Follow your own README instructions
3. Run all playbooks successfully
4. Verify vault encryption is working
5. Check that no sensitive data is exposed

## Resources

- [Ansible Vault Documentation](https://docs.ansible.com/ansible/latest/user_guide/vault.html)
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)

## FAQ

### Common Issues

1. **My vault file isn't encrypting properly**
   - Ensure you're using `ansible-vault create` or `encrypt` correctly
   - Verify the vault password is being entered correctly

2. **Playbooks fail to run**
   - Check if vault password is provided
   - Verify variable references are correct
   - Ensure all required files are in place

3. **GitHub shows my vault password**
   - Immediately change your vault password
   - Remove the file containing the password
   - Update `.gitignore`
   - Force push after cleaning history

### Best Practices Checklist

- [ ] No unencrypted sensitive data in repository
- [ ] `.gitignore` properly configured
- [ ] Clear documentation
- [ ] Proper variable references
- [ ] Multiple environment support
- [ ] Clean repository history

## Due Date

Submit your GitHub repository URL by [INSERT DATE]

## Questions?

If you have questions about this assignment, please contact [INSERT CONTACT INFO]

---
*Note: This is an educational assignment. Never commit real passwords or sensitive data to your repository.*
