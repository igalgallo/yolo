### IP-3 Project

## Tasks 

1. set up Application server 
2. Create Roles with 3 tasks as follows
3. Install docker
4. Clone repo
5. Docker compose
6. Test application if its created containers and application run.


### Set up Application server 
## Iniatiate vagrantfile and modify vagrantfile with  instruction to set up the Virtual boxTo create vagrantfile
#vagrant init 

#Then 
## create playbook.yml 
##  create ansible.cfg
## create hosts file

#### Create Roles with 3 Tasks as below

 ## Create Roles for each as below
 #ansible-galaxy role init roles/role name
 #ansible-galaxy role init roles/docker docker-installation
 #ansible-galaxy role init roles/clone-repo


## Modify Playbook for each Tasks for installation

 ## under each role  ,go to edit tasks -main.yml files and vars-main.yml


### Testing
## to bring up application
 #docker compose up 
## Run playbook to bring up vagrant 
 #vagrant provision

## Login to Vagrant VM by ssh below command
 
##galgee@devops:~/Documents/development/IP-2/yolo$ vagrant ssh
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.4.0-42-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
New release '22.04.2 LTS' available.
Run 'do-release-upgrade' to upgrade to it.

Last login: Mon Jul 31 18:50:01 2023 from 10.0.2.2

10. #Check docker image if created
vagrant@vagrant:~$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
mongo        latest    fb5fba25b25a   2 weeks ago   654MB
vagrant@vagrant:~$ 

vagrant@vagrant:~$ sudo docker ps -a
CONTAINER ID   IMAGE           COMMAND                  CREATED         STATUS         PORTS                                           NAMES
4d69355a899e   yolo-frontend   "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp       yolo-frontend-1
6fa03bb24da0   yolo-backend    "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp       yolo-backend-1
1f9683212790   mongo           "docker-entrypoint.s…"   5 minutes ago   Up 5 minutes   0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   yolo-mongodb-1
vagrant@vagrant:~$ 

