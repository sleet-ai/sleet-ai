# ssh

SSH key setup for GitHub and GitLab access from a new device

Run this on a device that does not already have an SSH key. The empty `-N` value creates the key without a passphrase.

```sh
# create the ~/.ssh directory if it does not already exist
mkdir -p ~/.ssh
# restrict the directory so only your user can read, write, or enter it
chmod 700 ~/.ssh
# generate a new Ed25519 key pair labeled sleet-ai@near.email with no passphrase
ssh-keygen -t ed25519 -C "sleet-ai@near.email" -f ~/.ssh/id_ed25519 -N ""
# lock down the private key so only your user can read or write it
chmod 600 ~/.ssh/id_ed25519
# let the public key remain readable by tools that need to fetch it
chmod 644 ~/.ssh/id_ed25519.pub
# start an SSH agent and load its environment settings into this shell
eval "$(ssh-agent -s)"
# register the private key with the agent so GitHub and GitLab can authenticate
ssh-add ~/.ssh/id_ed25519
# print the public key so it can be copied into GitHub and GitLab
cat ~/.ssh/id_ed25519.pub
```

The public key output is what you paste into the sleet-ai GitHub and GitLab accounts. Add it to the sleet-ai GitHub account at [GitHub SSH and GPG keys](https://github.com/settings/keys) using **New SSH key**. Add the same public key to the sleet-ai GitLab account at [GitLab SSH Keys](https://gitlab.com/-/user_settings/ssh_keys) using **Add new key**.

Only add the contents of `~/.ssh/id_ed25519.pub`. Never share or upload `~/.ssh/id_ed25519`.

Test access with:

```sh
# confirm SSH authentication with GitHub
ssh -T git@github.com
# confirm SSH authentication with GitLab
ssh -T git@gitlab.com
```

Use SSH repository URLs when cloning or changing remotes, such as `git@github.com:organization/repository.git` or `git@gitlab.com:group/repository.git`.

A key without a passphrase is convenient but less protected if the private key is copied. Keep the device secure, and be careful which repositories are granted to the sleet-ai GitHub and GitLab accounts because this key can access everything those accounts are permitted to access.

==================
<br/>
copyright 2026 by sleet.near
