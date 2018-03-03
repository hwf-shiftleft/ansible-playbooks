ansible-install
=========

Installs ansible on a host in a couple of ways

Requirements
------------

RHEL6/7

EPEL if using pip as the install type

Role Variables
--------------

## Required (outside of role):

None

## Defaults (with default values listed after the colon):

     ansible_role_install_type: package

The type of installation of ansible that should be performed.  Choose one of
 - package - use the O/S's package manager
 - pip - use pip
 - git - use git
 - dev - use git, and create a virtual environment for development

     ansible_install_git_dir: /opt/apps/ansible

The directory to install ansible into (when using git)

     ansible_install_venv_name: devel

The name of the virtual environment to create when using the 'dev' install method

     ansible_install_git_add_profile: false

Do we add a line to your profile that loads the ansible-specific binaries when using
'git' or 'dev'


     ansible_install_git_add_profile_locations: ['/etc/profile.d/ansible-setup.sh']

Where should we add a profile if using the add_profile pattern?

## Internal Vars

None

Dependencies
------------

None

Example Playbook
----------------


    - hosts: servers
      roles:
         - { role: ansible-install, ansible_install_type: pip }

License
-------

BSD

Author Information
------------------
John Walsh (mjohnw@med.umich.edu)
