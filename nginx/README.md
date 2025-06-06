# nginx

## Description

Nginx ("engine X") is a high-performance web and reverse proxy server created by
Igor Sysoev. It can be used both as a standalone web server and as a proxy to
reduce the load on back-end HTTP or mail servers.

For more information on the usage and available configuration options,
consult the following sections.

## Usage

### Install

```
- hosts: all
  roles:
    - role: nginx
  vars:
    nginx_state: 'install'
```

### Enable

```
- hosts: all
  roles:
    - role: nginx
  vars:
    nginx_state: 'enable'
```

### Disable

```
- hosts: all
  roles:
    - role: nginx
  vars:
    nginx_state: 'disable'
```

### Remove

```
- hosts: all
  roles:
    - role: nginx
  vars:
    nginx_state: 'remove'
```

### Inactive

```
- hosts: all
  roles:
    - role: nginx
  vars:
    nginx_state: 'inactive'
```

### Config

```
vars:
  nginx_config:
    - name: 'host.domain.tld'
      state: True
      hsts_state: True
      ssl_state: True
      ssl_certificate: '/etc/ssl/example/host.domain.tld.crt'
      ssl_certificate_key: '/etc/ssl/example/host.domain.tld.key'
      ssl_client_certificate: '/etc/ssl/example/ca.domain.tld.crt'
      ssl_verify_client: True
      ssl_verify_depth: 1
      config: |
        location / {
            proxy_pass                         https://localhost:8080;

            proxy_http_version                 1.1;
            proxy_redirect                     off;
            proxy_set_header Connection        "Upgrade";
            proxy_set_header Host              $host;
            proxy_set_header Upgrade           $http_upgrade;
            proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Host  $http_host;
            proxy_set_header X-Forwarded-Port  443;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Real-IP         $remote_addr;

            chunked_transfer_encoding          off;
            proxy_buffering                    off;
            proxy_connect_timeout              3600s;
            proxy_read_timeout                 3600s;
            proxy_send_timeout                 3600s;
            send_timeout                       3600s;

            client_max_body_size               0;
        }
```

## Parameters

### Config

`alias`

    Description: Define the 'alias' option.
    Required   : False
    Value      : Arbitrary
    Type       : Array
    Default    : []
    Options    :
      Examples: ['domain.tld', 'www.domain.tld', 'web.domain.tld]
      None    : []

`config`

    Description: Define the 'config' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : ''
    Options    :
      Examples: |
        location / {
            proxy_pass                         https://localhost:8080;

            proxy_http_version                 1.1;
            proxy_redirect                     off;
            proxy_set_header Connection        "Upgrade";
            proxy_set_header Host              $host;
            proxy_set_header Upgrade           $http_upgrade;
            proxy_set_header X-Forwarded-For   $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Host  $http_host;
            proxy_set_header X-Forwarded-Port  443;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Real-IP         $remote_addr;

            chunked_transfer_encoding          off;
            proxy_buffering                    off;
            proxy_connect_timeout              3600s;
            proxy_read_timeout                 3600s;
            proxy_send_timeout                 3600s;
            send_timeout                       3600s;

            client_max_body_size               0;
        }
      None: ''

`hsts_max_age`

    Description: Set the 'hsts_max_age' option.
    Required   : False
    Value      : Arbitrary
    Type       : Integer, String
    Default    : "{{nginx_hsts_max_age}}"
    Options    :
      Examples: 15768000 | 31536000 | 47304000

`hsts_state`

    Description: Control the 'hsts_state' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

`listen`

    Description: Define the 'listen' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : ['0.0.0.0', '[::]']
    Options    :
      Examples: ['*'] | ['127.0.0.1'] | '[:1]' | ['localhost']

`name`

    Description: Define the 'name' option.
    Required   : True
    Value      : Arbitrary
    Type       : String
    Default    : ''
    Options    :
      Examples: 'host.domain.tld'

`port`

    Description: Set the 'port' option.
    Required   : False
    Value      : Arbitrary
    Type       : Integer, String
    Default    : '443'
    Options    :
      Examples: '80' | '8080' | '443' | 8443'

`ssl_certificate`

    Description: Define the 'ssl_certificate_file' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : ''
    Options    :
      Examples: '/etc/ssl/example/host.domain.tld.crt'
      None    : ''

`ssl_certificate_key`

    Description: Define the 'ssl_certificate_key' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : ''
    Options    :
      Examples: '/etc/ssl/example/host.domain.tld.key'
      None    : ''

`ssl_ciphers`

    Description: Define the 'ssl_ciphers' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : 'ECDHE-RSA-CHACHA20-POLY1305:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-GCM-SHA256'
    Options    :
      Examples: 'TLS13-AES-256-GCM-SHA384:AES256+EECDH:AES256+EDH'

`ssl_client_certificate`

    Description: Define the 'ssl_client_certificate' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : ''
    Options    :
      Examples: '/etc/ssl/example/ca.domain.tld.crt'
      None    : ''

`ssl_ecdh_curve`

    Description: Define the 'ssl_ecdh_curve' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : 'secp521r1'
    Options    :
      Examples: 'secp384r1' | 'auto' | 'prime256v1:secp384r1'

`ssl_prefer_server_ciphers`

    Description: Control the 'ssl_prefer_server_ciphers' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : True
    Options    : True | False

`ssl_protocols`

    Description: Define the 'ssl_protocols' option.
    Required   : False
    Value      : Arbitrary
    Type       : Array
    Default    : ['TLSv1.2', 'TLSv1.3']
    Options    :
      Examples: ['TLSv1.3']

`ssl_session_tickets`

    Description: Control the 'ssl_session_tickets' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

`ssl_state`

    Description: Control the 'ssl_state' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

`ssl_verify_client`

    Description: Control the 'ssl_verify_client' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

`ssl_verify_depth`

    Description: Set the 'ssl_verify_depth' option.
    Required   : False
    Value      : Arbitrary
    Type       : Integer, String
    Default    : ''
    Options    :
      Examples: 1 | 2 | 3

`xss_protection_state`

    Description: Control the 'xss_protection_state' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

### Role

`nginx_state`

    Description: Control the state of the role.
    Required   : False
    Value      : Predetermined
    Type       : String
    Default    : 'enable'
    Options    :
      Install : 'true' | 'yes' | 'install'
      Enable  : 'start' | 'on' | 'enable'
      Disable : 'stop' | 'off' | 'disable'
      Remove  : 'false' | 'no' | 'remove'
      Inactive: 'quiesce' | 'inactive'

`nginx_config`

    Description: Define the 'nginx_config' option.
    Required   : False
    Value      : Arbitrary
    Type       : Array/Hash
    Default    : []
    Options    :
      Examples: [{name: 'host.domain.tld', state: True, hsts_state: True, ssl_state: True,
                 ssl_certificate: '/etc/ssl/example/host.domain.tld.crt',
                 ssl_certificate_key: '/etc/ssl/example/host.domain.tld.key',
                 ssl_client_certificate: '/etc/ssl/example/ca.domain.tld.crt',
                 ssl_verify_client: True,
                 ssl_verify_depth: 1}]
    None      : []

`nginx_hsts_max_age`

    Description: Set the 'nginx_hsts_max_age' option.
    Required   : False
    Value      : Arbitrary
    Type       : Integer, String
    Default    : '31536000'
    Options    :
      Examples: '15768000' | '31536000' | '47304000'

`nginx_log_format_main`

    Description: Define the 'nginx_log_format_main' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : |-
      '$remote_addr - $remote_user [$time_local] "$request" '
      '$status $body_bytes_sent "$http_referer" '
      '"$http_user_agent" "$http_x_forwarded_for"'
    Options    :
      Examples: |-
        'remote_addr:$remote_addr - $remote_user [$time_local] request:"$request" '
        'status:$status $body_bytes_sent "$http_referer" '
        '"$http_user_agent" http_x_forwarded_for:"$http_x_forwarded_for"'

`nginx_log_format_main_ssl`

    Description: Define the 'nginx_log_format_main_ssl' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : |-
      '$remote_addr - $remote_user [$time_local] "$request" '
      '$status $body_bytes_sent "$http_referer" '
      '"$http_user_agent" "$http_x_forwarded_for" '
      '$ssl_protocol/$ssl_cipher '
    Options    :
      Examples: |-
        'remote_addr:$remote_addr - $remote_user [$time_local] request:"$request" '
        'status:$status $body_bytes_sent "$http_referer" '
        '"$http_user_agent" http_x_forwarded_for:"$http_x_forwarded_for" '
        '$ssl_protocol/$ssl_cipher '

`nginx_monitor_monit_state`

    Description: Control the 'nginx_monitor_monit_state' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

`nginx_nftables_filter_rule`

    Description: Define the 'nginx_nftables_filter_rule' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : |
      add rule ip filter INPUT ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 } ct state new tcp dport { 80, 443 } counter accept comment "http, https from internal private addresses"
      add rule ip6 filter INPUT ip6 saddr fc00::/7 ct state new tcp dport { 80, 443 } counter accept comment "http, https from unique local addresses"
    Options    :
      Examples: |
        add rule ip filter INPUT ip saddr 10.0.0.0/8 ct state new tcp dport { 80, 443 } counter accept comment "http, https from internal-networks"

`nginx_nftables_state`

    Description: Control the 'nginx_nftables_state' option.
    Required   : False
    Value      : Predetermined
    Type       : Boolean
    Default    : False
    Options    : True | False

`nginx_vhosts_d`

    Description: Define the 'nginx_vhosts_d' option.
    Required   : False
    Value      : Arbitrary
    Type       : String
    Default    : 'vhosts.d'
    Options    :
      Examples: 'vhosts.d'

`nginx_worker_connections`

    Description: Set the 'nginx_worker_connections' option.
    Required   : False
    Value      : Arbitrary
    Type       : Integer, String
    Default    : 1024
    Options    :
      Examples: 256 | 512 | 1024 | 2048

## Conflicts

## Dependencies

### Packages

`nginx`

    Version: >= 1.8
    Name   :
      Debian 11: 'nginx'
      Debian 12: 'nginx'

`openssl`

    Version: >= 1.0
    Name   :
      Debian 11: 'openssl'
      Debian 12: 'openssl'

## Requirements

### Control Node

`ansible`

    Version: >= 2.15.0

### Managed Node

`python`

    Version: >= 3.10.0

## Support

### Operating Systems

`debian`

    Version: 11
    Version: 12
