Icinga Director Ansible Playbooks
================================

Introduction
------------

This document provides an illustrative guide to managing services in Icinga Director using sample Ansible playbooks inside this directory which leverage the `telekom_mms.icinga_director` Ansible collection.
The playbooks described here are intended as examples, designed to demonstrate potential use cases and provide a basis for custom playbook development.
It's important to note that these examples are not meant to be deployed without modifications.
These playbooks include management for the lifecycle of icinga object, including creation, update and delete, to make the Ansible configuration the SPoT.



How to Use
----------


The playbook includes three tasks and a role that is executed thereafter:

1. **Include Vars**: This task includes variables from the `vars/icinga_service.yml` file.

2. **Get All Object Configs**: This task retrieves all object configurations from the Icinga Director. The `url`, `url_username`, and `url_password` variables are used to authenticate with the Icinga Director. The `query` variable is set to `"*"` to retrieve all object configurations. The result is registered in the `result` variable.

3. **Create Objects Scheduled for Deletion**: This task creates objects that are scheduled for deletion. The `icinga_services` variable is updated with the services that are not currently in the `icinga_services` list but are present in the `result` objects. The new services are set to `'absent'` state.

In addition to these tasks, the playbook uses the `ansible_icinga` role.

Variables
---------

The playbook uses the following variables:

- `icinga_host`: The URL of the Icinga Director.
- `icinga_user`: The username used for authentication with the Icinga Director.
- `icinga_pass`: The password used for authentication with the Icinga Director.
- `icinga_services`: A list of services managed by the playbook. This variable should be defined in the `vars/icinga_service.yml` file.
- `icinga_force_basic_auth`: A boolean variable that forces basic authentication. This variable is set to `true`.

Make sure to define these variables before running the playbook.

Running the Playbook
--------------------

To run the playbook, use the `ansible-playbook` command.:

.. code-block:: bash

   ansible-playbook playbook.yml

Replace `playbook.yml` with the path to your playbook file.

Conclusion
----------

This playbook provides a simple way to manage services in Icinga Director. Make sure to customize the variables according to your environment before running the playbook.