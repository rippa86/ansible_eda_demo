deploy-security-demo
=========

This role tears down a demo setup in AAP. It removes the following structure:

* Organization: Rapid
  * Team: Rapid Admin (roles against Organization-Rapid: project_admin, notification_admin, inventory_admin, credential_admin, execution_environment_admin, auditor)
    * User: alfa (roles: member, read)
  * Team: Rapid Users (roles against Organization-Rapid: read, execute, auditor, job_template_admin)
    * User: zulu (roles: member, read)
  * Inventory: Rapid Assets
    * Host: {{ managed_host }}
  * Credential: Rapid Network Access (machine credential)
  * Project: Rapid Deployment (https://github.com/derekwaters/ansible_security_rapid with sync)
  * Job Template: Debug (with Rapid Network Access credential Rapid Assets inventory and debug.yml playbook)

Requirements
------------

This role requires a previously setup demo organization named "Rapid", and an admin account with access to remove organizations and
organization-owned objects.

Role Variables
--------------

aap_host: The hostname of the AAP controller instance
aap_username: A username of a user with administrative access to the AAP controller instance
aap_password: A password for a user with administrative access to the AAP controller instance

managed_host: The name of a managed host to be removed from the sample Inventory in AAP

Dependencies
------------

Depends on the following roles:
* ansible.controller
* containers.podman

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: derekwaters.teardown-security-demo, aap_host: controller.local, aap_username: admin, aap_password: password, managed_host: dummy_host.rapid.net }

License
-------

BSD

Author Information
------------------

Derek Waters (dwaters@redhat.com)
