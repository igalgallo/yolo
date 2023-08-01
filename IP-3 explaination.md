### P-3 Project
Tasks 
1. set up Application server 
2. Create Roles with 3 tasks as follows
3. Install docker
4. Clone repo
5. Docker compose
6. Test application if its run


 1. to create vagrantfile
#vagrant init 
 
 
2.Modify and configure vagrant file as below
 ===========
 # All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). 
 Vagrant.configure("2") do |config|
 # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
 config.vm.box = "geerlingguy/ubuntu2004"
 
 Create a private network, which allows host-only access to the machine
  # using a specific PORT.
  
  config.vm.network "private_network", type: "dhcp"
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  
  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  
  
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.config_file = "ansible.cfg"
    ansible.playbook = "playbook.yml"
  end
 end
 
 3. create palybook.yml
===================================
 ---
- name:  sample_yolo_playbook
  hosts:  all
  become:  yes
  roles:
    - docker-installation
    - clone-repo

  tasks:
    - name: run docker docker-compose.yaml
      command: docker compose up -d
      args:
        chdir: /home/vagrant/yolo


        ============================================
 4. create ansible.cfg
 ==================
 [defaults]
inventory = hosts
remote_user = vagrant
host_key_checking = False
=============================

 5. create hosts file
 ==========
 [webservers]
ip3.com ansible_ssh_port=2222 ansible_ssh_host=127.0.1.1 ansible_ssh_user='vagrant'

 ##ip3.com ansible_host=127.0.0.1 ansible_port=2222
 =============================
 
 6. then create a role using this command  for server_installation in the playbook.yml

 Create Roles for each as below
 #ansible-galaxy role init roles/role name
 ansible-galaxy role init roles/docker docker-installation
 ansible-galaxy role init roles/clone-repo

 #under each role  ,go to edit tasks -main.yml files and vars-main.yml

7.#to bring up application
 #docker compose up 


 8. Run playbook to bring up vagrant 
 #vagrant provision

9. #Login to Vagrant VM by ssh below command
 
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

