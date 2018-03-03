service-now-api
=========

An ansible role for interacting with service-now

Requirements
------------


Role Tags
---------

    create

Creates an item in the API

    read

Reads an item or group of items from the API

    update

Updates an item in the API

    delete

Deletes an item in the API

    debug

Adds lots of debug output for troubleshooting

Role Variables
--------------
# Required (outside of role )

    service_now_api_password: example_value

The password for authentication to servicenow

Brief description of its purpose and usage

# Optional (outside of role )

    service_now_api_body:
      assignment_group: Service Desk
      category: Software
      short_description: "FIXME NOW "
      caller_id: "Abraham Lincoln"
      comments: "Fix this up please.\nI've got a lot to do"

A basic body (in yaml format) that matches up to the fields of
the table in question
    
# Defaults
# Internal Vars


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: service-now-api }

License
-------

BSD

Author Information
------------------
John Walsh (mjohnw@med.umich.edu)
