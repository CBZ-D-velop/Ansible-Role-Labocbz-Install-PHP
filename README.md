# Ansible role: labocbz.install_php

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Crombez-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: Redis](https://img.shields.io/badge/Tech-Redis-orange)
![Tag: SSL/TLS](https://img.shields.io/badge/Tech-SSL%2FTLS-orange)
![Tag: PHP](https://img.shields.io/badge/Tech-PHP-orange)
![Tag: PHP-FPM](https://img.shields.io/badge/Tech-PHP--FPM-orange)

An Ansible role to install and configure PHP on your host.

## Folder structure

By default Ansible will look in each directory within a role for a main.yml file for relevant content (also man.yml and main):

```PYTHON
.
├── README.md  # Contains an overview of the role and its purpose.
├── defaults
│   ├── main.yml  # Contains default variables for the role that can be overridden by users.
│   └── README.md  # Contains documentation for the default variables.
├── files
│   └── README.md  # Contains documentation for the files in the directory.
├── handlers
│   ├── main.yml  # Contains handlers that can be called by tasks within the role.
│   └── README.md  # Contains documentation for the handlers.
├── meta
│   ├── main.yml  # Contains metadata about the role, including dependencies and supported platforms.
│   └── README.md  # Contains documentation for the role metadata.
├── tasks
│   ├── main.yml  # Contains tasks to be executed by the role on the managed nodes.
│   └── README.md  # Contains documentation for the tasks.
├── templates
│   └── README.md  # Contains documentation for the templates.
└── vars
    ├── main.yml  # Contains variables that are specific to the role and are not meant to be overridden.
    └── README.md  # Contains documentation for the role variables.
```

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the role) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This role contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your role
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this role, just copy/import this role or raw file into your fresh playbook repository or call it with the "include_role/import_role" module.

## Usage

### Vars

Some vars a required to run this role:

```YAML
---
install_php_version: "8.2"
install_php_version_is_default: true
install_php_install_fpm: true
install_php_import_cli_conf: true
install_php_import_apache_conf: true
install_php_import_cgi_conf: true
install_php_import_fpm_conf: true

install_php_max_input_time: 60
install_php_output_buffering: 4096
install_php_cgi_fix_pathinfo: 1
install_php_expose_php: "Off"
install_php_max_execution_time: 30
install_php_memory_limit: "512M"
install_php_post_max_size: "512M"
install_php_file_uploads: "On"
install_php_upload_max_filesize: "1024M"
install_php_max_file_uploads: 20
install_php_allow_url_fopen: "Off"
install_php_allow_url_include: "Off"
install_php_smtp: "localhost"
install_php_smtp_port: 25
install_php_session_save_handler: "files" # redis
install_php_session_save_path: "/var/lib/php/sessions" #tcp://127.0.0.1:6379?auth=<PASSWORD>
install_php_session_auto_start: 0
install_php_session_use_strict_mode: 0

install_php_extensions:
  - "php{{ install_php_version }}-zip"
  - "php{{ install_php_version }}-fpm"
  - "php{{ install_php_version }}-cli"
  - "php{{ install_php_version }}-mysql"
  - "php{{ install_php_version }}-gd"
  - "php{{ install_php_version }}-imagick"
  - "php{{ install_php_version }}-tidy"
  - "php{{ install_php_version }}-xmlrpc" 
  - "php{{ install_php_version }}-xml"
  - "php{{ install_php_version }}-redis"
  - "php{{ install_php_version }}-curl"
  - "php{{ install_php_version }}-dom"
  - "php{{ install_php_version }}-exif"
  - "php{{ install_php_version }}-fileinfo"
  - "php{{ install_php_version }}-cgi"
  - "php{{ install_php_version }}-mbstring"
  - "php{{ install_php_version }}-mysqli"
  - "php{{ install_php_version }}-bcmath"
  - "php{{ install_php_version }}-iconv"
  - "php{{ install_php_version }}-simplexml"
  - "php{{ install_php_version }}-xmlreader"
  - "php{{ install_php_version }}-ssh2"
  - "php{{ install_php_version }}-ftp"
  - "php{{ install_php_version }}-sockets"

install_php_disable_functions:
  - "phpinfo"
  - "system"
  - "exec"
  - "posix_uname"
  - "eval"
  - "pcntl_wexitstatus"
  - "posix_getpwuid"
  - "xmlrpc_entity_decode"
  - "pcntl_wifstopped"
  - "pcntl_wifexited"
  - "pcntl_wifsignaled"
  - "phpAds_XmlRpc"
  - "pcntl_strerror"
  - "ftp_exec"
  - "pcntl_wtermsig"
  - "mysql_pconnect"
  - "proc_nice"
  - "pcntl_sigtimedwait"
  - "posix_kill"
  - "pcntl_sigprocmask"
  - "fput"
  - "system"
  - "phpAds_remoteInfo"
  - "ftp_login"
  - "inject_code"
  - "posix_mkfifo"
  - "highlight_file"
  - "escapeshellcmd"
  - "show_source"
  - "pcntl_wifcontinued"
  - "fp"
  - "pcntl_alarm"
  - "pcntl_wait"
  - "ini_alter"
  - "posix_setpgid"
  - "parse_ini_file"
  - "ftp_raw"
  - "pcntl_waitpid"
  - "pcntl_getpriority"
  - "ftp_connect"
  - "pcntl_signal_dispatch"
  - "pcntl_wstopsig"
  - "ini_restore"
  - "ftp_put"
  - "passthru"
  - "proc_terminate"
  - "posix_setsid"
  - "pcntl_signal"
  - "pcntl_setpriority"
  - "phpAds_xmlrpcEncode"
  - "pcntl_exec"
  - "ftp_nb_fput"
  - "ftp_get"
  - "phpAds_xmlrpcDecode"
  - "pcntl_sigwaitinfo"
  - "shell_exec"
  - "pcntl_get_last_error"
  - "ftp_rawlist"
  - "pcntl_fork"
  - "posix_setuid"

```

The best way is to modify these vars by copy the ./default/main.yml file into the ./vars and edit with your personnals requirements.

You can set vars in the template model in Ansible AWX / Tower or just surchage them during the playbook call.

In order to surchage vars, you have multiples possibilities but for mains cases you have to put vars in your inventory and/or on your AWX / Tower interface.

```YAML
# From inventory
---
inv_install_php_version: "8.2"
inv_install_php_version_is_default: true
inv_install_php_install_fpm: true
inv_install_php_import_cli_conf: true
inv_install_php_import_apache_conf: true
inv_install_php_import_cgi_conf: true
inv_install_php_import_fpm_conf: true

inv_install_php_max_input_time: 60
inv_install_php_output_buffering: 4096
inv_install_php_cgi_fix_pathinfo: 0
inv_install_php_expose_php: "Off"
inv_install_php_max_execution_time: 30
inv_install_php_memory_limit: "4096M"
inv_install_php_post_max_size: "4096M"
inv_install_php_file_uploads: "On"
inv_install_php_upload_max_filesize: "4096M"
inv_install_php_max_file_uploads: 20
inv_install_php_allow_url_fopen: "Off"
inv_install_php_allow_url_include: "Off"
#inv_install_php_session_save_handler: "redis"
#inv_install_php_session_save_path: "tcp://{{ inventory_hostname }}:6379?auth=mySecret"

inv_install_php_session_save_handler: "redis"
inv_install_php_session_save_path: "tls://{{ inventory_hostname }}:6379?auth=mySecret"

#inv_install_php_session_save_handler: "rediscluster"
#inv_install_php_session_save_path: "seed[]=tls://ip1:port&seed[]=tls://ip2:port&stream[verify_peer]=0&stream[local_cert]=file:///path/to/cert.pem"

inv_install_php_session_auto_start: 0
inv_install_php_session_use_strict_mode: 0

inv_install_php_extensions:
  - "php{{ install_php_version }}-zip"
  - "php{{ install_php_version }}-fpm"
  - "php{{ install_php_version }}-cli"
  - "php{{ install_php_version }}-mysql"
  - "php{{ install_php_version }}-gd"
  - "php{{ install_php_version }}-imagick"
  - "php{{ install_php_version }}-tidy"
  - "php{{ install_php_version }}-xmlrpc" 
  - "php{{ install_php_version }}-xml"
  - "php{{ install_php_version }}-redis"
  - "php{{ install_php_version }}-curl"
  - "php{{ install_php_version }}-dom"
  - "php{{ install_php_version }}-exif"
  - "php{{ install_php_version }}-fileinfo"
  - "php{{ install_php_version }}-cgi"
  - "php{{ install_php_version }}-mbstring"
  - "php{{ install_php_version }}-mysqli"
  - "php{{ install_php_version }}-bcmath"
  - "php{{ install_php_version }}-iconv"
  - "php{{ install_php_version }}-simplexml"
  - "php{{ install_php_version }}-xmlreader"
  - "php{{ install_php_version }}-ssh2"
  - "php{{ install_php_version }}-ftp"
  - "php{{ install_php_version }}-sockets"

inv_install_php_disable_functions:
  #- "phpinfo"
  - "system"
  - "exec"
  - "posix_uname"
  - "eval"
  - "pcntl_wexitstatus"
  - "posix_getpwuid"
  - "xmlrpc_entity_decode"
  - "pcntl_wifstopped"
  - "pcntl_wifexited"
  - "pcntl_wifsignaled"
  - "phpAds_XmlRpc"
  - "pcntl_strerror"
  - "ftp_exec"
  - "pcntl_wtermsig"
  - "mysql_pconnect"
  - "proc_nice"
  - "pcntl_sigtimedwait"
  - "posix_kill"
  - "pcntl_sigprocmask"
  - "fput"
  - "system"
  - "phpAds_remoteInfo"
  - "ftp_login"
  - "inject_code"
  - "posix_mkfifo"
  - "highlight_file"
  - "escapeshellcmd"
  - "show_source"
  - "pcntl_wifcontinued"
  - "fp"
  - "pcntl_alarm"
  - "pcntl_wait"
  - "ini_alter"
  - "posix_setpgid"
  - "parse_ini_file"
  - "ftp_raw"
  - "pcntl_waitpid"
  - "pcntl_getpriority"
  - "ftp_connect"
  - "pcntl_signal_dispatch"
  - "pcntl_wstopsig"
  - "ini_restore"
  - "ftp_put"
  - "passthru"
  - "proc_terminate"
  - "posix_setsid"
  - "pcntl_signal"
  - "pcntl_setpriority"
  - "phpAds_xmlrpcEncode"
  - "pcntl_exec"
  - "ftp_nb_fput"
  - "ftp_get"
  - "phpAds_xmlrpcDecode"
  - "pcntl_sigwaitinfo"
  - "shell_exec"
  - "pcntl_get_last_error"
  - "ftp_rawlist"
  - "pcntl_fork"
  - "posix_setuid"

```

```YAML
# From AWX / Tower
---

```

### Run

To run this role, you can copy the molecule/default/converge.yml playbook and add it into your playbook:

```YAML
- name: "Include labocbz.install_php"
    tags:
    - "labocbz.install_php"
    vars:
    install_php_version: "{{ inv_install_php_version }}"
    install_php_version_is_default: "{{ inv_install_php_version_is_default }}"
    install_php_extensions: "{{ inv_install_php_extensions }}"
    install_php_install_fpm: "{{ inv_install_php_install_fpm }}"
    install_php_import_cli_conf: "{{ inv_install_php_import_cli_conf }}"
    install_php_import_apache_conf: "{{ inv_install_php_import_apache_conf }}"
    install_php_import_cgi_conf: "{{ inv_install_php_import_cgi_conf }}"
    install_php_import_fpm_conf: "{{ inv_install_php_import_fpm_conf }}"
    install_php_max_input_time: "{{ inv_install_php_max_input_time }}"
    install_php_output_buffering: "{{ inv_install_php_output_buffering }}"
    install_php_cgi_fix_pathinfo: "{{ inv_install_php_cgi_fix_pathinfo }}"
    install_php_expose_php: "{{ inv_install_php_expose_php }}"
    install_php_max_execution_time: "{{ inv_install_php_max_execution_time }}"
    install_php_memory_limit: "{{ inv_install_php_memory_limit }}"
    install_php_post_max_size: "{{ inv_install_php_post_max_size }}"
    install_php_file_uploads: "{{ inv_install_php_file_uploads }}"
    install_php_upload_max_filesize: "{{ inv_install_php_upload_max_filesize }}"
    install_php_max_file_uploads: "{{ inv_install_php_max_file_uploads }}"
    install_php_allow_url_fopen: "{{ inv_install_php_allow_url_fopen }}"
    install_php_allow_url_include: "{{ inv_install_php_allow_url_include }}"
    install_php_session_save_handler: "{{ inv_install_php_session_save_handler }}"
    install_php_session_save_path: "{{ inv_install_php_session_save_path }}"
    install_php_session_auto_start: "{{ inv_install_php_session_auto_start }}"
    install_php_session_use_strict_mode: "{{ inv_install_php_session_use_strict_mode }}"
    install_php_disable_functions: "{{ inv_install_php_disable_functions }}"
    ansible.builtin.include_role:
    name: "labocbz.install_php"
```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-08-10: First Init

* First init of this role with the bootstrap_role playbook by Lord Robin Crombez
* Role install PHP with the package manager
* PHP-\<version\> is installed
* Role can handle multiple version, so the possibility to set one as default is available
* Role create links to binary to use multiple version, as php-8.3 -v for php 8.3
* Role handle the installation of multiple extension, defaults are basic WordPress / Symfony requirements

## Authors

* Lord Robin Crombez

## Sources

* [Ansible role documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
* [How To Install PHP](https://tecadmin.net/how-to-install-php-on-debian-11/)
* [PHP extensions that WordPress needs to run properly](https://zeropointdevelopment.com/required-php-extensions-for-wordpress-wpquickies/)
