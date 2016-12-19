# Elastic Stack 5.x

An Ansible role for Ubuntu 14.04 that installs

- Oracle Java 8 (pre-req for all the things)
- Elasticsearch
- Logstash
- Beats
- Kibana

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
generic and flexible, we have gone the route of leaving the `copy` command as an empty dictionary.
It expects a list of dictionaries that contain a `src` key pointed to a local file and a `dest` key 
pointed to a destination path to be created with the source file.

```yaml
- role: elastic-stack-5.x
  install_java: yes
  install_logstash: yes
  ls_confd_files:
    - src: ansible/files/my-pattern-1.conf
      dest: /etc/logstash/conf.d/my-pattern-1.conf
    - src: ansible/files/my-pattern-2.conf
      dest: /etc/logstash/conf.d/my-pattern-2.conf
```
