# Ansible Collection - rikuson.lambda\_cloud\_infra

## Installation

Add collection into your `requirements.yml`.

```yaml
collections:
  - name: https://github.com/rikuson/lambda-cloud-infra.git
    type: git
    version: main
```

Run install command.

```shell
ansible-galaxy install -r requirements.yml
```

Update `ansible.cfg` to skip host key checking.

```
[defaults]
host_key_checking = False
```

## Usage

Prerequisites:

- Generate API key
- Add SSH key
- Create file system

```yaml
---
- hosts: localhost
  roles:
    - rikuson.lambda_cloud_infra.gpu_instance:
      vars:
        api_key: XXXXXXXXX
        instance_type: gpu_1x_a10
        region_name: us-west-1
        ssh_key_name: Macbook Air
        file_system_name: data
        host_groups: gpu_instance
- hosts: gpu_instance
  roles:
    - rikuson.lambda_cloud_infra.terminator:
      vars:
        api_key: XXXXXXXXX
        file_system_mount_point: /home/ubuntu/data
        output_file: /path/to/output/*[^__temp].mp4
        max_running_time: 24 hours
    - rikuson.lambda_cloud_infra.daemon:
      vars:
        name: daemon_name
        command: python run.py
        directory: /path/to/repo
```
