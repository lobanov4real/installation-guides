## All the commands you need in one place

Remove welcome ssh message:  
```bash
touch ~/.hushlogin
```  
  
Update the package lists and upgrade of all packages currently installed:  
```bash
sudo apt update && sudo apt upgrade -y
``` 
  
### Install docker

By script:
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
Manualy:
Add Docker’s official GPG key:  
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```  
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```  
```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```  
  
Set up the repository:  
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
``` 
  
Update the apt package index:  
```bash
sudo apt update
```  
  
Install Docker Engine, containerd, and Docker Compose:  
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```  

### Add your user to the docker group for run the Docker daemon as a non-root user (Rootless mode):  
```bash
sudo usermod -aG docker $USER
```  

Relogin to your user:
```bash
su $USER
```  

### Check versions of Docker and Docker compose:
```bash
docker version
```  
```bash
docker compose version
```  
