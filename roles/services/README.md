### Installs the services to test log collection

You simply need to specify inside **log-generator.yml** playbook waht services you wish to install using ```install_services``` variable:

Part of **log-generator.yml** playbook:
```
vars:
  install_services:
    - apache2 # uncomment a service to install
    # - nginx
```
