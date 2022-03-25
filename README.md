# Overview

This blueprint shows how to run a generic Ansible playbook via Cloudify, with the playbook and its variables specified as inputs.

It is intended only as an example to show how user input (passed via the UI, CLI, or API) could be used to run any Ansible playbook.

# Usage

To run the playbook, simply upload and run the blueprint. This can be done in one command from the CLI:

```
$ cfy install ansible-playbook.yaml
```

This will run the [create-tmpfile](./playbooks/create-tmpfile.yaml) playbook, which simply creates a file in `/tmp` on the Cloudify manager. The name of the file is specified as input.

The blueprint can also be run with the [delete-tmpfile](./playbooks/delete-tmpfile.yaml) playbook, which deletes the specified temporary file.

As an example of running the create and delete playbooks from the command line:

```
# Inputs file for the CLI action
$ cat /tmp/inputs.yaml
playbook_name: create-tmpfile.yaml
ansible_variables:
  file_name: created-by-ansible


# Create and run a deployment of the blueprint, passing in the desired inputs
$ cfy deployment create -b Ansible-Playbook -i /tmp/inputs.yaml 
$ cfy execution start -d Ansible-Playbook install

# Update the deployment to use a new playbook, which will triger a re-run of Ansible with the new playbook
$ cat /tmp/inputs.yaml
playbook_name: delete-tmpfile.yaml
ansible_variables:
  file_name: created-by-ansible
```
