# ansible-role-repo_setup

**This ansible role is to setup YUM repos from multiple sources.**

TODO: We need a way to make it possible to also remove all other repos.


## Installation

To install the role, create `requirements.yaml` with this content:

    - name: repo_setup
      src: https://github.com/jhutar/ansible-role-repo_setup.git
      version: origin/main

and then to install the role:

    ansible-galaxy install -r requirements.yaml --roles-path roles/

Now the role is available in `roles/repo_setup/`.

Check `repo_setup.yaml` for example on how to use the role in the playbook.


## Configuration

TODO


### Default variables

* `TODO` TODO


## References

1. TODO
