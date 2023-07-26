## All the commands you need in one place

Remove welcome ssh message:  
```
touch ~/.hushlogin
```  
  
Update the package lists and upgrade of all packages currently installed:  
```
sudo apt update && sudo apt upgrade -y
``` 
  
### Install docker
Add Docker’s official GPG key:  
```
sudo install -m 0755 -d /etc/apt/keyrings
```  
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```  
```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```  
  
Set up the repository:  
```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
``` 
  
Update the apt package index:  
```
sudo apt update
```  
  
Install Docker Engine, containerd, and Docker Compose:  
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```  

### Add your user to the docker group for run the Docker daemon as a non-root user (Rootless mode):  
```
sudo usermod -aG docker $USER
```  

Relogin to your user:
```su $USER
```  

### Check versions of Docker and Docker compose:
```
docker version
```  
```
docker compose version
```  
