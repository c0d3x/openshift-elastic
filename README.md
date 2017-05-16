## Info
I created this repository to add updated YML templates for running Elasticsearch & Kibana in Minishift/Openshift.

And I will document issues that I run into, the solutions will be added within this page.

Work in progress!

#### Future updates:
- Fix Cluster issues
- Add support for Logstash

# Docker Setup
To setup Docker in Linux Mint 18.1:

    #Docker Install:
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"

    sudo apt-get update

    sudo apt-get install docker-ce

    #Test Docker:
    sudo docker run hello-world

    #Manage Docker as a non-root user:
    sudo groupadd docker
    sudo usermod -aG docker $USER

    #Reboot System:
    sudo shutdown -r now

    #Docker-compose Install:
    sudo su
    curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    exit
    sudo chmod +x /usr/local/bin/docker-compose

    #Test Docker-compose:
    docker-compose --version

# Minishift Setup
When using template in Minishift for testing purposes, you might want this setup:

    #Install the repository:
    https://github.com/minishift/minishift/releases

    #Set VM-Driver to Virtualbox:
	minishift config set vm-driver virtualbox

    #Stop and delete current Minishift if any:
	minishift stop
	minishift delete

	#Add root user support:
	minishift addons install --defaults
	minishift addons enable anyuid

	#Add more Memory:
	minishift config set memory 8096

	#Start MiniShift Environment:
	minishift start

# OC - Command Line Interface

    #Login Administrator:
    oc login -u system:admin

    #Create Template from YML file to all projects:
    oc create -f elastic-template.yml -n openshift

    #Delete all templates:
    oc delete templates --all