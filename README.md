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


## Configuration

Check `repo_setup.yaml` for example on how to use the role in the playbook.

This role is configured by `additional_repos` variable that contains list
of repo definitions for all the repos you want to configure. For example:

    - name: "Test repo_setup"
      include_role:
        name: repo_setup
      vars:
        additional_repos:
          # Create repofile same way as yum_repository module does it
          - name: repo1
            description: My repo repo1
            baseurl: http://repos.example.com/repo1/
            gpgcheck: no
          # Download and install RPM (with GPG check disabled for package installation)
          # that provides the repo file
          - from_rpm: https://repos.example.com/repo2-latest.noarch.rpm
            disable_gpg_check: yes
          # Just download existing repofile
          - from_file: http://repos.example.com/repo3/repo3.repo
          # Download existing repo file and also import CA certificate
          - from_file: http://repos.example.com/repo4/repo4.repo
            needs_cert: http://repos.example.com/ca.crt
          # Download existing repo file and fix baseurl line in it
          - from_file: http://repos.example.com/repo5/repo5.repo
            fix_regexp: baseurl *= *https://example.com/repo5/
            fix_line: baseurl=https://repos.example.com/repo5/


### Default variables

* when adding repo using config, repo is created with `gpgcheck` enabled
  if not specified otherwise (use `gpgcheck: no` to disable it)
* for repos installed `from_rpm`, by default gpgcheck is enabled when
  the RPM is being installed. This is OK when RPM is signed with key
  imported to rpm (use `disable_gpg_check: yes` to disable it)


## References

1. <https://docs.ansible.com/ansible/latest/collections/ansible/builtin/yum_repository_module.html>
