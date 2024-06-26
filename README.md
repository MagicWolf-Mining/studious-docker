This guide will show you how to install Docker to Ubuntu server in proxmox environment.

What is Docker?
Docker is an open-source platform that enables developers to automate the deployment of applications inside lightweight, portable containers.
Containers are isolated environments that contain everything needed to run an application, including the code, runtime, system tools, libraries, and settings. 
Docker provides a way to package and distribute applications along with their dependencies, making it easier to build, ship, and run applications across different environments.

Installing Docker on Ubuntu is relatively straightforward. Here are the steps:

1. Update Package Index:
Before installing any new software, it's a good practice to update the local package index to ensure you have the latest versions of available packages:

		sudo apt update
		sudo apt upgrade

2. Install Required Packages:
Install the packages necessary to allow apt to use a repository over HTTPS:

		sudo apt install apt-transport-https ca-certificates curl software-properties-common

optional cmd for same as above

		sudo apt install curl apt-transport-https ca-certificates

You will notice that we are installing three additional packages. Each of them is quite useful for the following steps.

curl – We will be using curl to fetch the gpg key for the Ubuntu versions of Docker. curl allows us to pipe this key directly to the apt package manager.

apt-transport-https – By default, the apt package manager does not have support for the HTTPS protocol.

By installing this package, we will be able to interact with the official Docker repository, which is served over HTTPS.

ca-certificates – The final package we install is the bundle of certificates. These certificates are what helps the system know that the website it is connecting to is who they say they are.
 
3. Add Docker's GPG Key:
Add Docker's official GPG key to ensure the integrity of downloaded Docker packages:

		curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

optional same function as 3 above (3. Our next step is to add the GPG key for the Ubuntu repository to our keyrings directory.
This key is used to verify that the packages you are installing are from that repository.

		curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/docker-archive-keyring.gpg >/dev/null
)

4. Add Docker Repository:
Add the Docker repository to your system's software sources list:

		sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"


optional link use with step 3 optional cmd

		echo "deb [signed-by=/usr/share/keyrings/docker-archive-keyring.gpg arch=$(dpkg --print-architecture)] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee -a /etc/apt/sources.list.d/docker.list

6. Update Package Index Again:
Update the package index once more to ensure apt is aware of the Docker packages now available from the newly added repository:

		sudo apt update

7. Install Docker Engine:
Install the latest version of Docker Engine:

		sudo apt install docker-ce

8. Verify Docker Installation:
Check that Docker has been installed correctly by running the following command, which should output the installed version:

		docker --version

From this, you should get the version of docker that you have installed to your system. The message should look a bit like what we have below
	
 Docker version 20.10.6, build 370c289

8. Manage Docker as a Non-Root User (Optional):
By default, Docker commands require sudo privileges. If you want to run Docker commands without sudo, you can add your user to the docker group:

		sudo usermod -aG docker $USER

You'll need to log out and back in or restart your system for this change to take effect.

9. Start and Enable Docker Service:
Start the Docker service and enable it to start on boot:

		sudo systemctl start docker
		sudo systemctl enable docker

That's it! Docker should now be installed and running on your Ubuntu system. You can start using Docker to create and manage containers.

If you want Docker to boot up at the same time as when your Ubuntu system does, you need to enable its service.

You can enable the service by running the command on your system.

		sudo systemctl enable docker

 The Docker service is automatically enabled during the installation process.

Disabling the Docker Service
If you have issues with Docker or do not want to have it automatically startup, you need to disable the service.

Disabling the service is as straightforward as using the following command.

		sudo systemctl disable docker

 As Docker is running as a service, you may want to check on its status from time to time.

Systemctl keeps track of all services running on your Ubuntu system. This allows you to see whether the software is currently running or crashed.

		sudo systemctl status docker


Install Docker Compose


To install Docker Compose on Ubuntu, you can follow these steps:

1. Download Docker Compose Binary:
First, you need to download the Docker Compose binary into your system's PATH. You can replace version_number with the version you want to install.
To find the latest release, visit the Docker Compose GitHub releases page.

To check the status of Docker on your Ubuntu system, you can use the following command within the terminal.

		sudo curl -L "https://github.com/docker/compose/releases/download/version_number/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

2. Add Execute Permissions:
Make the downloaded binary executable:

		sudo chmod +x /usr/local/bin/docker-compose

4. Verify Installation:
Check that Docker Compose has been installed correctly by running:

		docker-compose --version

This command should output the installed version of Docker Compose.

That's it! Docker Compose should now be installed on your Ubuntu system and ready to use. You can start using Docker Compose to define and run multi-container Docker applications.



Cleaning Up
If you need to uninstall Docker, run the following

		sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras




		

