Kryp7ik Filebeat
=========

This role will install and configure Filebeat, Metricbeat & Packetbeat on CentOS / RHEL 7 hosts.

Requirements
------------

Should have an ELK server installed so filebeat can be configured to communicate with it.

Role Variables
--------------

    # hostname or IP of the elk server ( make sure this matches the bind address/hostname configured on elasticsearch and/or logstash )
    elk_server: 'elk.krynet.com'
    
    # Specify which output methods you would like to use
    beats_output_elastic: True
    beats_output_logstash: False
    
    # Output ssl configuration
    # automatically retrieve certificate and key from ipa server
    ipa_getcert: True
    beats_ssl_ca: '/etc/ipa/ca.crt'
    beats_ssl_cert: '/etc/pki/tls/certs/{{ inventory_hostname }}.pem'
    beats_ssl_key: '/etc/pki/tls/private/{{ inventory_hostname }}.key'
    
    # Elastic output settings
    beats_elastic_protocol: 'https'
    beats_elastic_username: 'elastic'
    beats_elastic_password: 'changeme'
    
    # Logstash output settings
    beats_logstash_ssl: True
    
    # Ansible will automatically check each host to see if the packages that correspond to a module are installed and if so it will add them to the config file.
    # You can disable this feature by setting service_auto_check to false
    service_auto_check: True
    
    # --------------- FILEBEAT -------------------------------------------------
    install_filebeat: True
    
    # filebeat configuration option of where to retrieve log files
    # NOTE: you may not want to include log files that would be retrieved by one of the filebeat modules
    filebeat_log_paths:
      - '/var/log/*.log'
    
    # Filebeat modules.  If you're using the service_auto_check ansible will automatically enable the relevant modules
    filebeat_modules:
      system:
        enabled: True
        config: '- module: system'
      apache:
        enabled: False
        config: '- module: apache2'
      auditd:
        enabled: False
        config: '- module: auditd'
      mysql:
        enabled: False
        config: '- module: mysql'
      nginx:
        enabled: False
        config: '- module: nginx'
    
    
    # --------------- PACKETBEAT ------------------------------------------------
    # Given you may not want to install packetbeat on every server the default is set to False
    # You should override this variable in the host_vars for the hosts you want packetbeat to installed on.
    install_packetbeat: False
    
    # Network interface to use.
    packetbeat_interfaces: 'any'
    
    # Ports packetbeat should listen to
    packetbeat_http_ports: [80, 443, 8080, 8000, 5000, 8002]
    packetbeat_amqp_ports: [5672]
    packetbeat_cassandra_ports: [9042]
    packetbeat_dns_ports: [53]
    packetbeat_memcache_ports: [11211]
    packetbeat_mysql_ports: [3306]
    packetbeat_pgsql_ports: [5432]
    packetbeat_redis_ports: [6379]
    packetbeat_thrift_ports: [9090]
    packetbeat_mongodb_ports: [27017]
    packetbeat_nfs_ports: [2049]
    
    # --------------- METRICBEAT -------------------------------------------------
    install_metricbeat: True
    
    # These are the services that ansible will automatically detect and enable when using service_auto_check
    # If it discovers that the service is installed it will automatically set the enabled variable to True
    # If your not using service_auto_check you can set the 'enabled' variable(s) that correspond to the modules you want enabled to True
    mb_modules:
      mb_system:
        enabled: True
        config: |
          - module: system
            metricsets:
              - cpu
              - filesystem
              - fsstat
              - memory
              - network
              - process
              - socket
            enabled: true
            period: 10s
            processes: ['.*']
      mb_apache:
        enabled: False
        config: |
          - module: apache
            metricsets: ["status"]
            enabled: true
            period: 10s
            hosts: ["http://127.0.0.1"]
      mb_ceph:
        enabled: False
        config: |
          - module: ceph
            metricsets: ["cluster_disk", "cluster_health", "monitor_health", "pool_disk"]
            enabled: true
            period: 10s
            hosts: ["localhost:5000"]
      mb_couchbase:
        enabled: False
        config: |
          - module: couchbase
            metricsets: ["cluster", "node", "bucket"]
            enabled: true
            period: 10s
            hosts: ["localhost:8091"]
      mb_docker:
        enabled: False
        config: |
          - module: docker
            metricsets: ["container", "cpu", "diskio", "healthcheck", "info", "memory", "network"]
            hosts: ["unix:///var/run/docker.sock"]
            enabled: true
            period: 10s
            ssl:
              certificate_authority: "/etc/pki/root/ca.pem"
              certificate: "/etc/pki/client/cert.pem"
              key: "/etc/pki/client/cert.key"
      mb_haproxy:
        enabled: False
        config: |
          - module: haproxy
            metricsets: ["info", "stat"]
            enabled: true
            period: 10s
            hosts: ["tcp://127.0.0.1:8080"]
      mb_jolokia:
        enabled: False
        config: |
          - module: jolokia
            metricsets: ["jmx"]
            enabled: true
            period: 10s
            hosts: ["localhost"]
            namespace: "metrics"
            path: "/jolokia/?ignoreErrors=true&canonicalNaming=false"
            jmx.mapping:
            jmx.application:
            jmx.instance:
      mb_mongodb:
        enabled: False
        config: |
          - module: mongodb
            metricsets: ["status"]
            hosts: ["localhost:27017"]
            username: root
            password: test
      mb_mysql:
        enabled: False
        config: |
          - module: mysql
            metricsets: ["status"]
            enabled: true
            period: 10s
            hosts: ["root:secret@tcp(127.0.0.1:3306)/"]
      mb_nginx:
        enabled: False
        config: |
          - module: nginx
            metricsets: ["stubstatus"]
            enabled: true
            period: 10s
            hosts: ["http://127.0.0.1"]
      mb_php_fpm:
        enabled: False
        config: |
          - module: php_fpm
            metricsets: ["pool"]
            enabled: true
            period: 10s
            status_path: "/status"
            hosts: ["localhost:8080"]
      mb_postgresql:
        enabled: False
        config: |
          - module: postgresql
            metricsets: ["database", "bgwriter", "activity"]
            enabled: true
            period: 10s
            hosts: ["postgres://localhost:5432"]
            username: user
            password: pass
      mb_prometheus:
        enabled: False
        config: |
          - module: prometheus
            metricsets: ["stats"]
            enabled: true
            period: 10s
            hosts: ["localhost:9090"]
            metrics_path: /metrics
            namespace: example
      mb_redis:
        enabled: False
        config: |
          - module: redis
            metricsets: ["info", "keyspace"]
            enabled: true
            period: 10s
            hosts: ["127.0.0.1:6379"]
      mb_zoo_keeper:
        enabled: False
        config: |
          - module: zookeeper
            metricsets: ["mntr"]
            enabled: true
            period: 10s
            hosts: ["localhost:2181"]

Dependencies
------------

None

Example Playbook
----------------

    - hosts: elk_beats
      remote_user: username
      become: yes
      become_method: sudo
      roles:
        - { role: filebeat, tags: 'filebeat' }

License
-------

BSD
