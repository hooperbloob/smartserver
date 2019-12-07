# Smartserver

This project contains my complete automated IoT Server deployment setup.

[http://www.intranet-of-things.com/smarthome/infrastructure/server/setup/](http://www.intranet-of-things.com/smarthome/infrastructure/server/setup/)

## Requirements

Just install [vagrant](https://www.vagrantup.com/) and run:

```bash
vagrant up test
```
It will deploys a test machine running inside virtual box.


To deploy an environment similar to my production system, run:

```bash
vagrant up develop_suse

```

or if you want to try a beta version of my new fedora based deployment, run:

```bash
vagrant up develop_fedora
```

Both (Suse and Fedora) are depending on some encrypted vagrant vault files. :-)


You can also use the contained ansible files directly.

```bash
# run everything in production
ansible-playbook -i server.ini -l production --ask-vault-pass server.yml

# run everything in production except vault depending tasks
ansible-playbook -i server.ini -l production server.yml

# run nextcloud in production
ansible-playbook -i server.ini -l production --tags "nextcloud" --ask-vault-pass  server.yml

# run nextcloud in production without vault depending tasks
ansible-playbook -i server.ini -l production --tags "nextcloud"  server.yml


# run everything in staging
ansible-playbook -i server.ini -l develop --ask-vault-pass server.yml

# run everything in staging except vault depending tasks
ansible-playbook -i server.ini -l develop server.yml

# run nextcloud in staging
ansible-playbook -i server.ini -l develop --tags "nextcloud" --ask-vault-pass  server.yml

# run nextcloud in staging without vault depending tasks
ansible-playbook -i server.ini -l develop --tags "nextcloud"  server.yml


# run everything in test environment
ansible-playbook -i server.ini -l test server.yml
```
