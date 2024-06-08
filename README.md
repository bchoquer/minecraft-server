# minecraft-server
CS312 Minecraft server automated deployment

## Background: 
We want to create a minecraft server that is basically automatically set up by our Ansible scripts and Docker. 
Our main goals are:
- Write provisioning for AWS.
- Create configuration and deployment scripts for a Minecraft server.

This will be done using Ansible to set up our AWS resources, then deploy a Minecraft docker image and use the minecraft.service file to set up automatic restarts. 

## Requirements:
 - Ansible 
 - Docker 
 - apt 
 - SSH keys set up in AWS 
 - ~/.aws/credentials file with current login creds
 - Minecraft security group setup in AWS 

## Broad overview of the different steps/stages of the pipeline:
AWS instance -> Runs Docker -> Dockcer runs Minecraft server -> minecraft systemd service file runs on container 

## Tutorial to Run the Code

**Step 1: Provision Minecraft AWS instance**
```sh
ansible-playbook provision_aws.yml
```

**Step 2: Install and configure Docker**
```sh
ansible-playbook -i /tmp/ansible-inventory/hosts configure_docker.yaml
```

**Step 3: Start Minecraft**
```sh
ansible-playbook -i /tmp/ansible-inventory/hosts run_minecraft.yaml
```

**Step 4: Once the Minecraft server is running, connect to the instance using the public IP provided by the scripts.**


## Resources/Sources Used
- [itzg/minecraft-server](https://hub.docker.com/r/itzg/minecraft-server)
- Several Reddit threads:
  - [Reddit Thread 1](https://www.reddit.com/r/aws/comments/1402x80/cant_start_my_ec2_instance_status_goes_to_pending/)
  - [Reddit Thread 2](https://www.reddit.com/r/aws/comments/14v3qov/ec2_instance_killed_when_attempting_to_run_a/)
  - [Stack Overflow Thread](https://stackoverflow.com/questions/60806200/how-would-i-create-a-minecraft-ec2-server-that-automaticaly-starts-when-someone)
- [How to setup Minecraft server on Ubuntu 18.04 Bionic Beaver Linux](https://linuxconfig.org/how-to-setup-minecraft-server-on-ubuntu-18-04-bionic-beaver-linux)
- [Connect to a Linux instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html)
