# Ansible Role: Graylog Sidecar

This role installs and configures the Graylog Sidecar agent on RHEL/CentOS, Debian/Ubuntu and Fedora servers.

## Here be Dragons!

This role adds the Elasticsearch repository to the managed system to install beats. Make sure you are not breaking existing repository configuration with this!

## Requirements

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: foobar
      roles:
        - role: ansible-role-graylog-sidecar
          become: yes

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    graylog_sidecar_version: 1.0.2

Set the Graylog Sidecar version to install.

    graylog_sidecar_config:
      server_url: http://localhost:9000/api
      server_api_token: foo-bar-baz-bar-foo
      node_name: "{{ ansible_hostname }}"

Configure the Sidecar. The list can be expanded with any option recognized by Graylog Sidecar.

    graylog_sidecar_beats:
      - filebeat
      - journalbeat

List which beats should be installed from the elasticsearch repository. **Currently there are only handlers for the beats in the example, but that can be easily expanded.**

## Dependencies

None.

## OS Compatibility

This role ensures that it is not used against unsupported or untested operating systems by checking, if the right distribution name and major version number are present in a dedicated variable named like `<role-name>_stable_os`. You can find the variable in the role's default variable file at `defaults/main.yml`:

    common_stable_os:
      - Debian 10
      - Ubuntu 18
      - CentOS 7
      - Fedora 30

If the combination of distribution and major version number do not match the target system, the role will fail. To allow the role to work add the distribution name and major version name to that variable and you are good to go. But please test the new combination first!

Kudos to [HarryHarcourt](https://github.com/HarryHarcourt) for this idea!

## Example Playbook

    ---
    - name: "Run role."
      hosts: all
      become: yes
      roles:
        - ansible-role-graylog-sidecar

## Contributing

Please feel free to open issues if you find any bugs, problems or if you see room for improvement. Also feel free to contact me anytime if you want to ask or discuss something.

## Disclaimer

This role is provided AS IS and I can and will not guarantee that the role works as intended, nor can I be accountable for any damage or misconfiguration done by this role. Study the role thoroughly before using it.

## License

MIT

## Author Information

This role was created in 2020 by [Thorian93](http://thorian93.de/).
