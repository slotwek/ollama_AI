---
date: 2026-09-12
aliases:
relates_to:
---
## Check if the ollama is already running:
*Look for **127.0.0.1:11434** and its PID: 12968 (in this case).*
> ![cmd netstat -ano with findstr.png](https://raw.githubusercontent.com/slotwek/ollama_AI/main/ollama/attachments/cmd%20netstat%20-ano%20with%20findstr.png)

- So, something is listening on port **:11434** - with **PID 12968** (the last value is PID). 

## Let's check what is the PID:
> ![cmd tasklist with PID equal_to number.png](https://raw.githubusercontent.com/slotwek/ollama_AI/main/ollama/attachments/cmd%20tasklist%20with%20PID%20equal_to%20number.png)


# Let's check if the server is running
- If Ollama is running, you should get JSON containing your installed models.
> ![cmd curl localhost api tags.png](https://raw.githubusercontent.com/slotwek/ollama_AI/main/ollama/attachments/cmd%20curl%20localhost%20api%20tags.png)
