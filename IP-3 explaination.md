##  IP-3 Project


### Tasks 

1. set up Application server 
2. Create Roles with 3 tasks as follows
 Install docker,
 Clone repo,
 Docker compose.
3.  Test application if its created containers and application run.

## Set up Application server
### vagrant init 
This to iniatiate vagrantfile and modify vagrantfile with  instruction to set up the Virtual boxTo create vagrantfile

Then 
1. create playbook.yml 
2. create ansible.cfg
3. create hosts file

#### Create Roles
We need to create roles with eachs tasks as below ,which will creates different folders and modify main.yml for each task and vars files.

 1. ansible-galaxy role init roles/docker docker-installation
 2. ansible-galaxy role init roles/clone-repo



### Testing

1. docker compose up ; to bring up application
2. vagrant provision ;to run playbook to bring up vagrant
3. vagrant ssh ; to login to vagrant 
4. sudo docker images to check images created
5. sudo docker ps -a ; to check containers running and test application running.


