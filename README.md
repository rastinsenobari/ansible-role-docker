# Install docker with Ansible

Docker is one of the most famous and practical tools. You need to install it on any server you connect to.
With this playbook, you can install Docker in Ubuntu hosts and grant non-root access to yourself or other users.
> Please note that this playbook actually reinstalls your Docker engine if it was already installed. It removes all unofficial packages, but it does not delete your images, containers, volumes, or networks.

## Instructions

1. Clone this repository.

```bash
git clone https://github.com/rastinsenobari/install-docker-ansible && cd install-docker-ansible
```

2. Run the Ansible playbook.

```bash
ansible-playbook install-docker.yml -K
```
After executing the command, you need to enter a password to access "sudo" in order to apply changes to the system.

## Options
 - By default, this playbook grants the running user non-root access to execute Docker commands. If you wish to ignore this default behavior, you should run it like this:
```bash
ansible-playbook install-docker.yml -K --extra-vars "running_user_access='false'" 
```

 - If you want to grant non-root access to other users, you should add the users in the template and run the playbook like this:

```bash
ansible-playbook install-docker.yml -K --extra-vars "add_users_access='true'" 
```

```yaml
users:
  - user1
  - user2
```
change users.yml like this template

## Verification
Run the following command to check the installation:
```bash
docker run hello-world
```
 Note: If you encounter 'permission denied' due to lack of access, you should log out and log in again. Alternatively, you can use the following command.
```bash
su - $USER
```

> Pay attention: If the command does not run correctly, it's possible that you don't have access to Docker Hub. In such cases, consider using a Docker-registry-mirror or configuring DNS to pull images.


## Contributing

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue. Don't forget to give the project a star! Thanks again!