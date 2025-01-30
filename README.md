# deepseek
```
https://github.com/ollama/ollama  # curl -fsSL https://ollama.com/install.sh | sh
https://ollama.com/
```
## How to install deepseek
```
curl -fsSL https://ollama.com/install.sh | sh
ollama pull - wget https://ollama.com/library/deepseek-r1
ollama run deepseek-r1
```
## Example
```
cat test.py
import requests

# Change this to your VM's IP if running remotely
#OLLAMA_URL = "http://127.0.0.1:11434/api/generate"
#OLLAMA_URL = "http://127.0.0.1:11434/api/generate"
OLLAMA_URL = "http://10.0.112.15:8080/api/generate"

# Define the request payload
payload = {
    "model": "deepseek-r1",
    "prompt": "What is AI?",
    "stream": False  # Set to True for streaming responses
}

# Send request
response = requests.post(OLLAMA_URL, json=payload)

# Print the response
print(response.json())
```
## How to expose as API
```
pip install fastapi uvicorn requests

cat proxy.py
from fastapi import FastAPI
import requests

app = FastAPI()

OLLAMA_API = "http://127.0.0.1:11434"

@app.post("/api/generate")
async def generate(body: dict):
    """Proxy requests to Ollama API"""
    response = requests.post(f"{OLLAMA_API}/api/generate", json=body)
    return response.json()

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8080)

```
