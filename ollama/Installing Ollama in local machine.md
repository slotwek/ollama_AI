---
date: 2026-10-27
aliases:
relates_to:
---
Source: https://www.youtube.com/watch?v=Wjrdr0NU4Sk

# Steps:
## Windows Host:
1. Install wsl linux
	```cmd
	wsl --install
	```
2. Reboot
3. Install wsl linux - then it works correctly
	```cmd
	wsl --install
	```
	- I was able to set user and password. 
	- And I was immediately switched to Linux cli
4. Update the system:
	```bash
	# in WSL Linux
	sudo apt update
	sudo apt upgrade -y
	```
5. Then I've tried to install ollama:
	```bash
	curl -fsSL https://ollama.com/install.sh | sh
	```
	- however, I got an error, which said I need to install `zstd` first
6. Installing  zstd
	```bash
	sudo apt-get install zstd
	```
	- it was suggested to install it with `apt-get`
7. Then I've tried to install ollama:
	```bash
	curl -fsSL https://ollama.com/install.sh | sh
	```
	- and it worked!
8. Now, we can test on the Host machine following URL:
	```URL
	http://localhost:11434
	```
	- it should say that `Ollama is running`
9. Now, we can pull the models (you can skip to step 10 - immediately)
	```bash - wsl
	ollama pull llama2
	```
10. And run the model:
	```bash - wsl
	ollama run llama2
	```
11.  Install docker
```bash
networkchuck@deb-alien :~ $ # Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings /docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo
"deb [arch=$(dpkg -- print-architecture) signed-by=/etc/apt/keyrings/docker.asc]
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" |\
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
1. 

---
[ollama - main](https://github.com/slotwek/ollama_AI/blob/main/ollama%20-%20main.md)