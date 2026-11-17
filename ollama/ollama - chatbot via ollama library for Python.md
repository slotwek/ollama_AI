---
date: 2026-09-12
aliases:
relates_to:
---
# Install ollama library for Python
```bash
pip  install  ollama

# or:
pip3  install  ollama
```
> ![[cmd pip install ollama.png]]

# You can run ollama with command:
```shel
python package.py
```
> ![[python running ollama as script (chat).png]]

## package.py
*Content of the file:*
```python
import ollama

# Initialize the Ollama client
client = ollama.Client()

# Define the model and the input prompt
model = "llama2"  # Replace with your model name
prompt = "What is Python?"

# Send the query to the model
response = client.generate(model=model, prompt=prompt)

# Print the response from the model
print("Response from Ollama:")
print(response.response)
```

---
[[ollama - main]], [[ollama - chatbot over command prompt]]