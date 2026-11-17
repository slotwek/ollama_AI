---
date: 2026-09-12
aliases:
relates_to:
---
Source: [Teacher's Tech](https://www.youtube.com/watch?v=aQ1rblXB91U)
# Pre-requests:
- ollama - [[ollama - how to install]]
- gemma4 model

# Requirements:
- Open WebUI

# How does it work?
- ollama is the engine
- Open WebUI is the dashboard - this is just front end
	- it uses [[Docker]]
		- [Docker download link](https://www.docker.com/products/docker-desktop/)

After installing [[Docker]], **start Docker Desktop**. You should see screen similar to this one:
> ![[Docker GUI.png]]

After this run this command (use next command if you're using Obsidian!):
```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```
**Note!** Because Obsidian is using, use this command instead: 
```bash
docker run -d -p 3001:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

> [!multi-column] Installing
>> [!NOTE] Incorrectly
>> ![[Failed Docker Run.png]]
>
>> [!NOTE] Correctly - after starting Docker Desktop
>> ![[cmd docker run after running Docker Desktop.png]]
>

In web browser type:
```text
localhost:3000
```
> ![[Open WebUI over ollama.png]]

Because the command uses port **:3000**, it has a clash with Obsidian presentations! For now, I have closed the Obsidian and then it started working.

It will ask you for user name, e-mail address and password. But *is locally*. It is not send anywhere. 
![[Pasted image 20260912221001.png]]


> ![[Pasted image 20260912221847.png]]

# What if you need to delete and recreate stuff:
- Stop WebUI
```bash
docker stop open-webui
```
- Delete the docker:
```bash
docker rm open-webui
```
- And then you can type the command:
```bash
docker run -d -p 3001:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```
> ![[cmd docker run on port 3001.png]]

## This is what Docker Desktop shows:
> ![[Docker Desktop with 1 container.png]]

# Checking if it works:
> ![[WebUI ollama test.png]]

---
[[ollama - main]]