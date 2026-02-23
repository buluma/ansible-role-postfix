# [Ansible role postfix](#ansible-role-postfix)

Install and configure postfix on your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-postfix/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-postfix/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-postfix/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-postfix)|[![downloads](https://img.shields.io/ansible/role/d/buluma/postfix)](https://galaxy.ansible.com/buluma/postfix)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-postfix.svg)](https://github.com/buluma/ansible-role-postfix/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-postfix/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
  - become: true
    gather_facts: true
    hosts: all
    name: Converge
    roles:
      - postfix_aliases:
          - destination: test@example.com
            name: root
        postfix_mydomain: example.com
        postfix_myhostname: smtp.example.com
        postfix_mynetworks:
          - 127.0.0.0/8
          - 192.168.0.0/16
        postfix_myorigin: example.com
        postfix_relayhost: '[smtp.ziggo.nl]:587'
        postfix_smtp_sasl_auth_enable: true
        postfix_smtp_sasl_password_map: /etc/postfix/relay_pass
        postfix_smtp_sasl_password_map_content: '[smtp.ziggo.nl]:587 email-address:email-password

          '
        postfix_smtp_sasl_security_options: ''
        postfix_smtp_tls_security_level: may
        postfix_smtp_tls_wrappermode: false
        role: buluma.postfix
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-postfix/blob/master/molecule/default/prepare.yml):

```yaml
---
  - become: true
    gather_facts: false
    hosts: all
    name: Prepare
    roles:
      - role: buluma.bootstrap
      - role: buluma.core_dependencies
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-postfix/blob/master/defaults/main.yml):

```yaml
---
postfix_banner: $myhostname ESMTP $mail_name
postfix_inet_interfaces: loopback-only
postfix_inet_protocols: all
postfix_mydestination: $mydomain, $myhostname, localhost.$mydomain, localhost
postfix_mydomain: "{{ ansible_domain | default('localdomain', true) }}"
postfix_myhostname: "{{ ansible_fqdn }}"
postfix_mynetworks:
  - 127.0.0.0/8
postfix_myorigin: "{{ ansible_domain | default('localdomain', true) }}"
postfix_smtp_listen_port: smtp
postfix_smtp_sasl_auth_enable: false
postfix_smtp_sasl_password_map: ""
postfix_smtp_sasl_password_map_content: ""
postfix_smtp_sasl_security_options: ""
postfix_smtp_tls_security_level: none
postfix_smtp_tls_wrappermode: false
postfix_smtpd_recipient_restrictions:
  - permit_mynetworks
  - permit_sasl_authenticated
  - reject_unauth_destination
  - reject_invalid_hostname
  - reject_non_fqdn_hostname
  - reject_non_fqdn_sender
  - reject_non_fqdn_recipient
  - reject_unknown_sender_domain
  - reject_unknown_recipient_domain
  - reject_rbl_client sbl.spamhaus.org
  - reject_rbl_client cbl.abuseat.org
  - reject_rbl_client dul.dnsbl.sorbs.net
  - permit
postfix_smtpd_sender_restrictions:
  - reject_unknown_sender_domain
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-postfix/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-postfix/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Amazon](https://hub.docker.com/r/buluma/amazonlinux)|all|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|
|[Kali](https://hub.docker.com/r/buluma/kalilinux)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-postfix/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-postfix/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

