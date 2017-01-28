# Elastic Stack 5.x

An Ansible role for Ubuntu 14.04 that installs

- Oracle Java 8 (pre-req for all the things)
- Elasticsearch
- Logstash
- Beats
- Kibana
- XPack

## Usage

__NOTE:__ this does nothing by default! In order for anything to be installed, you must explicitly
tell Ansible to install it in the role configuration per playbook.

```yaml
- role: elastic-stack-5.x
  install_java: yes
  install_elasticsearch: yes
  install_logstash: yes
```

The above will install Java, ES and LS, but not install Beats or Kibana.

### Elasticsearch

```yaml
- role: elastic-stack-5.x
  install_java: yes
  install_elasticsearch: yes
```

### Logstash

Logstash is pretty useless without your user defined parser configs. In order to make this role
generic and flexible, we have gone the route of leaving the `template` command as an empty list
of paths.

You should define a list of fileglobs that will match the templates you want to copy.
Copying index templates (for elasticsearch mappings) is also supported via ls_grok_pattern_files.
Index templates and conf files are handled as j2 templates, and should end with the `.j2` extension.


Finally, static provisional files (like grok patterns, etc) may be listed under `ls_provisional_files`.
These files will be copied directly into the base logstash path (usually `/etc/logstash/`).
The provisional files/directories should be specified individually. They'll be copied directly as is.
Do not give a fileglob.

```yaml
- role: elastic-stack-5.x
  install_java: yes
  install_logstash: yes
  ls_confd_files:
    - /Users/vince/Workspace/test/ansible/templates/foo-*.conf.j2
    - /Users/vince/Workspace/test/ansible/templates/bar.conf.j2
  ls_index_template_files:
    - /path/to/the/things/*
  ls_provisional_files:
    - /path/to/grok/patterns/dir
    - /path/to/dictionary/dir
```


## TODO

- kibana
- xpack
- metricbeat
- packetbeat
- winlogbeat (?)
