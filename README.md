# phonebook-traefik for Ubuntu 22.04

1. Rename hosts.yml.dist to hosts.yml and add server address and username.

2. Rename server.yml.dist to server.yml and change username.

3. Rename authorize.yml.dist to authorize.yml and add change username and patch to public key.

3. Install

>cd provisioning && make server

4. Copy SSH key for user deploy on VM. 

>make authorize

4. Deploy treafik

>cd .. && HOST=server_ip PORT=ssh_port make deploy

5 Traefik network name: traefik-public