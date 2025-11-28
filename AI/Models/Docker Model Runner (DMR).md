# Docker Model Runner (DMR): A Simpler, Standardized Way to Run AI Models Anywhere

As AI workloads scale, teams often struggle with fragmented model environments, inconsistent inference setups, and complex deployment pipelines. Docker’s **Model Runner (DMR)** changes this by offering a **unified, plug-and-play runtime** designed specifically for packaging and serving machine-learning models — especially LLMs.

DMR modernizes how models are run: **no custom servers**, no dependency chaos, and no infrastructure lock-in. Just build → run → scale.

---

# What Is Docker Model Runner (DMR)?

**Docker Model Runner** is Docker’s official model execution runtime that lets you package and run models as containers with a standardized interface.

It gives you:

* ✔ A **standard model-serving API**
* ✔ Automatic **model discovery** and **weight loading**
* ✔ **Hardware-aware** execution (CPU / GPU / multi-GPU)
* ✔ Built-in **token streaming** for LLMs
* ✔ Unified architecture for **local dev → cloud → Kubernetes**
* ✔ A reproducible runtime for any model format (GGUF, ONNX, PyTorch, TFLite, etc.)

DMR's purpose is **portability** and **uniformity** — no matter which model you run or which hardware you deploy to.

---

# Why Docker Created Model Runner

Traditional ML serving has challenges:

* Every model has its own dependencies
* Every ML engineer builds their own server
* GPU environments are complex
* Scaling requires re-architecting
* Local dev and production differ

DMR solves this with a single runtime that:

1. **Understands models**
2. **Exposes a consistent API**
3. **Handles device optimization**
4. **Works everywhere you run Docker**

This makes DMR the “Dockerfile of AI models.”

---

# How DMR Works Internally

At runtime, DMR:

1. Detects your model (LLM, embedding model, vision model)
2. Loads the model weights
3. Selects the correct backend (CPU, GPU, CUDA, ROCm, etc.)
4. Initializes the inference engine
5. Exposes APIs like:

   * `/generate`
   * `/embeddings`
   * `/v1/chat/completions`
   * `/health`
   * `/metrics`

It removes the need to write FastAPI/Flask/TGI/vLLM servers manually.

---

# Running a Model with DMR

This is where DMR shines — **zero setup**.

### **1. Pull the Model Runner Image**

```
docker pull docker/model-runner:latest
```

### **2. Run a Model**

```
docker run -p 8000:8000 \
    -v ./models:/models \
    docker/model-runner --model /models/llama-3.1-8b
```

DMR auto-detects the model type and starts the API server.

### **3. Query the Model**

```
curl http://localhost:8000/v1/chat/completions \
   -d '{ "model": "llama-3.1-8b", "messages": [{"role": "user", "content": "Hello"}] }'
```

Done. No Python. No server code. No CUDA setup.

---

# Key Features of Docker Model Runner

### **1. Standardized OpenAI-Compatible API**

DMR supports `/v1/chat/completions`, `/v1/completions`, `/v1/embeddings`.

You can swap OpenAI → local model by changing just the base URL.

---

### **2. Token Streaming Built-In**

DMR supports real-time token streaming:

* SSE streaming
* Web-based streaming
* CLI streaming

Perfect for LLM chat apps.

---

### **3. Hardware-Aware Execution**

DMR automatically uses:

* CPU
* NVIDIA GPU (CUDA)
* AMD GPU (ROCm)
* Multi-GPU setups

No reconfiguration required.

---

### **4. Multi-Model Hosting**

Serve multiple models in the same DMR instance with routing rules.

---

### **5. Production Readiness**

DMR includes:

* `/health/live`
* `/health/ready`
* `/metrics`
* Structured logs
* Tracing hooks

Built for Kubernetes & container platforms.

---

## ✅ Core `docker model` Commands

| Command                             | Description / Purpose                                                                                                                                                          |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `docker model install-runner`       | Install Docker Model Runner (needed on some setups, e.g. Docker Engine on Linux). ([Docker Documentation][2])                                                                  |
| `docker model uninstall-runner`     | Uninstall Docker Model Runner (i.e. remove the plugin/runner). ([Docker Documentation][1])                                                                                     |
| `docker model version`              | Show the version of Docker Model Runner (check what version of DMR you have). ([Docker Documentation][1])                                                                      |
| `docker model list`                 | List all AI/ML models you have pulled / that are locally available for running. ([Docker Documentation][1])                                                                    |
| `docker model pull <MODEL>`         | Pull/download a model (from Docker Hub, HuggingFace or an OCI registry) to make it available locally. ([Docker Documentation][1])                                              |
| `docker model push <MODEL>`         | Push a model (OCI-artifact) to Docker Hub (or another registry). Useful if you’ve packaged or tagged a model and want to share. ([Docker Documentation][1])                    |
| `docker model package`              | Package a model file (e.g. a `.gguf` file) into a Docker-model OCI artifact — optionally specify license, context-size, and push it to a registry. ([Docker Documentation][1]) |
| `docker model run <MODEL> [PROMPT]` | Run the model, either giving a prompt for one-off execution, or in interactive chat mode if no prompt provided. ([Docker Documentation][3])                                    |
| `docker model inspect <MODEL>`      | Display detailed information about a specific model (metadata, tags, maybe config) available locally. ([Docker Documentation][1])                                              |
| `docker model logs`                 | Fetch or stream logs from Model Runner — useful for debugging or monitoring inference activity. ([Docker Documentation][1])                                                    |
| `docker model status`               | Check if Docker Model Runner is currently running (its daemon/service status). ([Docker Documentation][1])                                                                     |
| `docker model tag SOURCE TARGET`    | Retag a local model (or OCI-artifact) under a new name — e.g. to push under a different namespace. ([Docker Documentation][1])                                                 |
| `docker model rm <MODEL>`           | Remove a local model (delete the downloaded model) to free up space. ([Docker Documentation][1])                                                                               |

---

## 🔧 Example Usage & Options

* To **run a model**:

```
docker model run ai/some-model "Hello, how are you?"
```

or, for interactive mode:

````
docker model run ai/some-model
``` :contentReference[oaicite:15]{index=15}

- To **package a GGUF model file** and push to a registry:

````

docker model package --gguf /path/to/model.gguf --push myorg/my-model:tag

```:contentReference[oaicite:16]{index=16}

- To **pull** a model from a public registry:

```

docker model pull ai/smollm2:latest

```:contentReference[oaicite:17]{index=17}

- To **check status** of the runner:

```

docker model status

```:contentReference[oaicite:18]{index=18}

---

# Example: Llama 3.1 with DMR

```
docker run --gpus all \
  -p 8000:8000 \
  -v $PWD/models:/models \
  docker/model-runner \
  --model /models/Meta-Llama-3.1-70B-Instruct
```

DMR optimizes:

* KV cache
* CUDA allocation
* Streaming
* Parallel sampling

You get near vLLM-level efficiency with almost zero configuration.

---

# DMR in the Cloud

You can deploy DMR anywhere Docker runs:

### Kubernetes

Just wrap it in a Deployment + Service YAML.

### AWS ECS / Fargate

Push to ECR → scale tasks.

### Azure Container Apps

DMR handles everything internally.

### Docker Desktop

Use it for local experiments with GPU passthrough.

---

# Why DMR Matters for ML Teams

Teams love DMR because it:

### ✔ Eliminates custom inference servers

### ✔ Standardizes model interfaces

### ✔ Works across all clouds

### ✔ Makes local → prod seamless

### ✔ Reduces DevOps + ML Ops complexity

### ✔ Speeds up model deployment 10×

DMR is Docker’s answer to:

* messy ML deployment pipelines
* unmaintainable Python servers
* inconsistent runtime environments

---

# Final Thoughts

Docker Model Runner (DMR) isn’t just a tool — it’s a **new standard** for running AI models anywhere, in a predictable and scalable way.

It brings:

* Consistent inference APIs
* GPU-aware execution
* Zero boilerplate
* Zero infrastructure lock-in
* Clean portability from laptop to Kubernetes

If your organization runs multiple models — or you use LLMs heavily — DMR becomes a game-changer.
