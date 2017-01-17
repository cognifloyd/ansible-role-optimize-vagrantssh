# Ansible Role: Optimize connections for Vagrant-managed RHEL/CentOS boxes

[![Build Status](https://travis-ci.org/cognifloyd/ansible-role-optimize-vagrantssh.svg?branch=master)](https://travis-ci.org/cognifloyd/ansible-role-optimize-vagrantssh)

This role optimizes the vm (RHEL/CentOS) for speedy vagrant connections.

This role was forked from geerlingguy.packer-rhel v1.2.2 (e392ebc).

## Requirements

!!! warning "This is out of date!"

Prior to running this role via Packer, you need to make sure Ansible is installed via a shell provisioner, and that preliminary VM configuration (like adding a vagrant user to the appropriate group and the sudoers file) is complete, generally by using a Kickstart installation file (e.g. `ks.cfg`) with Packer. An example array of provisioners for your Packer .json template would be something like:

    "provisioners": [
      {
        "type": "ansible",
        "playbook_file": "ansible/main.yml",
        "role_paths": [
          "/home/cognifloyd/.galaxy/roles/cognifloyd.optimize-vagrantssh",
        ]
      }
    ],

The files should contain, at a minimum:

**ansible/main.yml**:

    ---
    - hosts: all
      become: true
      gather_facts: true
      roles:
        - cognifloyd.optimize-vagrantssh

You might also want to add another shell provisioner to run cleanup, erasing free space using `dd`, but this is not required (it will just save a little disk space in the Packer-produced .box file).

If you'd like to add additional roles, make sure you add them to the `role_paths` array in the template .json file, and then you can include them in `main.yml` as you normally would. The Ansible configuration will be run over a local connection from within the Linux environment, so all relevant files need to be copied over to the VM; configuratin for this is in the template .json file. Read more: [Ansible Local Provisioner](http://www.packer.io/docs/provisioners/ansible-local.html).

## Role Variables

None.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - { role: cognifloyd.optimize-vagrantssh }

## License

MIT / BSD

## Author Information

This role is based on the [geerlingguy.packer-rhel](https://galaxy.ansible.com/geerlingguy/packer-rhel/) role that was created in 2014 by [Jeff Geerling](http://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
