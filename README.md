# ansible-bootstrap-system
Ansible role used to setup a freshly created operating system

## Usage

### Remote syslog over TCP, htpdate and proxy

    - name: Do OS-ready configuration
      hosts: all
      roles:
        - role: bootstrap-system
      vars:
        bootstrap_syslog_target_host: my-syslog.local
        bootstrap_set_hostname_from_inventory: true

        bootstrap_htpdate_servers:
          - http://www.wikipedia.org

        bootstrap_http_proxy_packages_per_repo:
          - host: "archive.ubuntu.com"
            proxy: "http://my-proxy.local:3128"

### Remote GELF over HTTP with additional tags

    - name: Do OS-ready configuration
      hosts: all
      roles:
        - role: bootstrap-system
      vars:
        bootstrap_syslog_target_host: graylog.local
        bootstrap_syslog_target_port: 8080
        bootstrap_syslog_target_protocol: http
        bootstrap_syslog_additional_tags:
            environment: production
            tenant: my-custom-tenant
            cloud: amazon
            region: us-west-1
            az: seattle

### /etc/hosts configuration

    - name: Do OS-ready configuration
      hosts: all
      roles:
        - role: bootstrap-system
      vars:
        bootstrap_static_hosts:
           - ip: 1.2.3.4
             hosts:
               - www.example.org
               - example.org
