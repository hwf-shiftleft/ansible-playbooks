Hacks with Friends Ansible Playbooks 
===============

* This repository hosts the playbooks for UM Hacks with Friends

Standard Variables
=================

The following variable can be defined in the playbook if needed (with descriptions after each item):

    hostpath: "{{ host_files }}/{{ inventory_hostname }}"

Place host-specific files here
   
    grouppath: "{{ group_files }}/group-name"

Place group-specific files here.  This allows you to reference the "src" as grouppath that can be
overriden on an as-needed basis

    curr_env: "{{ inventory_file.split('/')|last }}"

The current tier/environment (see tiers section below)

Tiers
=====

We separate our inventory files into our standard tiers by default.  Our current process
is to add a pre-task to our playbook if we are clustering or using HA.  We create a variable
file in the group_vars directory with the same name as the inventory host group appended by 
"-{{ tier }}".  Something like the following:

    pre_tasks:
      - name: Include tier-specific variables
        include_vars: group_vars/{{ hosts }}-{{ curr_env }}.yml
        tags: always
