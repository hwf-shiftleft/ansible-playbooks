rundeck
=========

Install rundeck to a host

Requirements
------------

Tags
----

The following are the non standard tags in place for this role:

## restore

If this tag is added to the play, rundeck will try to restore the jobs
from the xml files located in the job directory.  Note, this is not
idempotent and may squash any changes if the server exists

## aclpolicy

If this tag is added, only changes to the admin.aclpolicy file are pushed to 
the rundeck server.

Role Variables
--------------
## Required (outside of role):

    rundeck_api_tokens:
      - user: username
        token: 1l2lo23no2mfoh23o4uyj013103jop34j0jef0

If you would like to use ansible-managed tokens, use this
list-of-dict format (user needs to exist).

    rundeck_job_load_token:

This token should be set if you use the "restore" tag in your playbook. It is the token
that is used to load the jobs into Rundeck

    rundeck_datasource_user:

The username to use for rundeck data source (not needed for default rundeck_datasource_url)

    rundeck_datasource_pass:

The password for the rundeck data source (not needed for default rundeck_datasource_url)

## Optional (outside of role):

    rundeck_framework_server_uuid

A uuid to identify this particular server for load-balancing or HA.


    rundeck_storage_converters:
     - type: jasypt-encryption
       path: /keys
       config:
         encryptorType: strong
         password: changeme1234

Sets up storage converters for rundeck.  type and path are required, any config element can
be used and the key will be added changed to the property.  The above variable will generate
the following in rundeck-config.properties:

    rundeck.storage.converter.1.type=jasypt-encryption
    rundeck.storage.converter.1.path=/keys
    rundeck.storage.converter.1.config.password=changeme1234
    rundeck.storage.converter.1.config.encryptorType=strong

## Defaults (with default values listed after the colon):

    localuser: rundeck

The user that the rundeck process runs as

    localgroup: rundeck

The group that the rundeck process runs as

    rundeck_config_dir: /etc/rundeck

The configuration directory for properties and other files

    rundeck_base_dir: /var/lib/rundeck

Equivalent to Rundeck's "BASE_DIR" - where rundeck lives and runs

    rundeck_tmp_dir: /tmp/rundeck/

A temp space for rundeck

    rundeck_jvm_settings: " -Xmx2g -Xms256m -XX:MaxPermSize=256m -server"

The default settings for the java virtual machine

    rundeck_login_module: MultiAuth

The login module to use.  A template must exist with the name "jaas-{{ rundeck_login_module }}.conf"
and defined with the same name inside the file.  See http://rundeck.org/docs/administration/authenticating-users.html
for more info and settings to configure

    rundeck_allow_api_full_perms: false

Allow anyone who has an api token to have the default permissions of rundeck 
(including job create and other stuff - be careful!).  
If this is set to false, you will need to set up project or job-level access on a per-user or api_token_group 
See this for more info:
http://rundeck.org/docs/administration/access-control-policy.html#special-api-token-authentication-group 


    rundeck_realm_users:
      - username: admin
        password: 'OBF:changeme'
        groups: user,admin,architect,deploy,build

Users to add to realm.properties file (used if you use FilePropertyLogin in your login_module) Note:
see the framework_user and framework_password variables below.  They assume the first user in the list
is the one that you should use for the framework settings.  See also rundeck documentation for types
of passwords allowed

    rundeck_framework_user: admin 

The username for connection to the rundeck server for shell tools and core rundeck services

    rundeck_framework_password: admin 

The password for connection to the rundeck server for shell tools and core rundeck services

    rundeck_http_port: 4440

The port for rundeck to listen to for non-encrypted requests

    rundeck_https_port: 4443

The port to listen to for encrypted connections

    rundeck_user: acduser

The default user to connect to remote hosts as

    rundeck_base_role: user

The base role that has rights to login to rundeck.  Can be a LDAP group if needed,
but you can also add supplementalRole to your login_module if you prefer.

    rundeck_gui_startpage: jobs

By default, show jobs when a user clicks on a project, versus the project homepage.
valid values: 'adhoc', 'configure', 'createJob', 'events', 'home', 'jobs', 'nodes', 'projectHome'

## Internal Vars:

Dependencies
------------
- apache
- install-ansible, with pip to take advantage of some options in 2.2 that was not released yet

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: rundeck }

License
-------

BSD

Author Information
------------------
John Walsh (mjohnw@med.umich.edu)
