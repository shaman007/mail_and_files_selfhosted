# own_hosted_cloud

UPD: this pet project moved to K8S

Ansible playbooks needed to install postfix, dovecot, greylisting, roundcube, wordpress, nextcloud on your own host. There are several bits and dimes that are related to my own host andreybondarenko.com, I am too lazy to make it 100% interportable and indempotent, please make a pull request if you have ideas.

  - Packages: install all rpms we will need.
  - User: create local user and put authorized keys.
  - Mysql: create evryting that is needed for the Wordpress instance and disable public network connections.
  - Wordpress: installation + upload plugin + import plugin. Settings and import of the previous content is possible only by hands.
  - Mail: postfix + opendkim + postgrey + dovecot + sieve
  - Reload: reload all services that we have.

TODO:
  - backup

Inventory file contains all secrets that are used and should be like:
```
own-cloud:
  hosts:
    example.com:
      host_ip: 91.26.66.70
      host_name: example.com
      user: your_user_name
      password: ******
      dkim_secret: "-----BEGIN RSA PRIVATE KEY-----\n
      MIICXQIBAAw3gQ3vG4Wf5PP6VI70f87P90+0sB4oL33mt1GBE/QRd3X5Izv1iAJF\n
      ...
      WuieXfd5k1w26dIPrpbVm2QHq4c4r15vS6AGJ9vwPsrp\n
      -----END RSA PRIVATE KEY-----"
      wp_secret: "define('AUTH_KEY',         ' ... ');\n
      define('SECURE_AUTH_KEY',  ' ... ');\n
      define('LOGGED_IN_KEY',    ' ... ');\n
      define('NONCE_KEY',        ' ... ');\n
      define('AUTH_SALT',        ' ... ');\n
      define('SECURE_AUTH_SALT', ' ... ');\n
      define('LOGGED_IN_SALT',   ' ... ');\n
      define('NONCE_SALT',       ' ... ');\n"
      auth_keys: ":ssh-rsa AA .. user@example.com"
      defautl_private: "-----BEGIN RSA PRIVATE KEY-----\n
      MIISXDIDAGKBgQCvGRWfWPPZVIg0fy7Pr0+rsBsoL6Imt1GBE/QRd3X5Izv1iAJF\n
      ...
      WuieXfd5k1226dI3rpbV5aQ6+4Kbr1nveMAGJ9vwPsrp\n
      -----END RSA PRIVATE KEY-----"
```
