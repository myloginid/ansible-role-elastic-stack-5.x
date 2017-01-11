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
of paths. You should define a list of absolute paths to the config files (for now at least).

```yaml
- role: elastic-stack-5.x
  install_java: yes
  install_logstash: yes
  ls_confd_files:
    - /Users/vince/Workspace/test/ansible/templates/ls-conf1.conf
    - /Users/vince/Workspace/test/ansible/templates/ls-conf2.conf
```


## TODO

- kibana
- xpack
- metricbeat
- packetbeat
- winlogbeat (?)
