# Ansible OSQuery role

This is the Ansible OSQuery + Prometheus Exporter role. It's designed for consumption by playbooks, not for consumption
by itself. It adds OSQuery and it's Prometheus exporter. It's expected that another role will take care of reverse
proxying this exporter with SSL and auth. 

## Dependencies

This assumes that the node exporter role has been installed and configured to look for exported metrics from batch
jobs in the standard location.

For more information, see 

// Todo: Put a link.

## Requirements

- Internet Access
- osquery_exporter compiled and available in ${GOPATH}/bin/

### Why is OSQuery needed locally

The OSQuery repo does not have any releases; it's built on HEAD. So, to limit the complexity of this playbook we
presume that:

- ${GOPATH} environment variable exists, and 
- osquery_exporter is in ${GOPATH}/bin/osquery_exporter

Whether it's the correct architecture is further beyond the scope of this playbook (i.e. if it's for a Raspberry Pi,
compile it for ARM)

## Usage

Include this in another ansible playbook. For sample, consider a generic server playbook:

```
---
# $PLAYBOOK_ROOT/server.yaml
- name: "server"
  hosts: all
  become: true
  become_user: "root"
```

Add the reference for the role:

```
# $PLAYBOOK_ROOT/server.yaml
# ...
become_user: "root"
roles
  - "osquery"
```

This will allow the role to be discovered. Then, add this repo as a submodule:

```
$ cd path/to/playbook/root
$ mkdir roles/
$ git submodule add https://github.com/littlemanco/ansible-role-osquery roles/osquery
```

This should work!

## Configuration

The variables that are available are defined in defaults/main.yml

## Design

### Why is OSQuery bundled with Prometheus exporter

Because that's how I felt like doing it. It feels like a small, but also, I don't care at the minute -- I'm just
playing around.

## Contact

- Contact: hello@andrewhowden.com
- Web: https://www.andrewhowden.com/
