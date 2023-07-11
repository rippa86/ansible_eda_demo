deploy-eda-demo
=========

This role creates a demo setup in AAP. It creates the following structure:

* Organization: midrange
  * Project: itsm-demo (https://github.com/derekwaters/ansible_eda_demo with sync)
  * Credential: test-cred
  * Host: test-host
  * Inventory: test-inventory (containing test-host)
  * Job Templates:
    * 1-create-cr
    * 2-prepatch-check
    * 3.0-update-cr-status-scheduled
    * 3.1-update-cr-status-started
    * 3.2-update-cr-status-failed
    * 3.3-update-cr-status-review
    * 3.4-update-cr-status-complete
    * 4-apply-patch
    * 5-postpatch-check
    * 6-rollback-patch
  * Workflow-Template: patch-workflow

Requirements
------------

This role requires an empty(ish) AAP environment, and an admin account with access to create organizations and
organization-owned objects.

Role Variables
--------------

aap_host: The hostname of the AAP controller instance
aap_username: A username of a user with administrative access to the AAP controller instance
aap_password: A password for a user with administrative access to the AAP controller instance

network_cred_username: A username for a user account used to create a sample Credential in AAP
network_cred_password: A password for a user account used to create a sample Credential in AAP

managed_host: The name of a managed host to be added to the sample Inventory in AAP

snow_hostname: The name of a ServiceNow host
snow_username: THe username of a ServiceNow user
snow_password: The password of a ServiceNow user


Dependencies
------------

Depends on the following roles:
* ansible.controller
* containers.podman

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: derekwaters.deploy-eda-demo, aap_host: controller.local, aap_username: admin, aap_password: password, network_cred_username: rapid_svc, network_cred_password: password, managed_host: dummy_host.rapid.net }

License
-------

BSD

Author Information
------------------

Derek Waters (dwaters@redhat.com)
