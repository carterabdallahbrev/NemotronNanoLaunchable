# Nemotron Nano 9B v2 NIM Setup

This repository contains a Jupyter notebook for setting up and running the NVIDIA Nemotron Nano 9B v2 model using NVIDIA NIM (NVIDIA Inference Microservices).

## Prerequisites

Before running the notebook, ensure you have:

1. **NVIDIA GPU** with appropriate drivers installed
2. **Docker** with GPU support (nvidia-docker/nvidia-container-toolkit)
3. **Python 3.8+** with Jupyter notebook support
4. **NGC API Key** - Get yours from [NVIDIA Build](https://build.nvidia.com/nvidia/nvidia-nemotron-nano-9b-v2/deploy)
5. Sufficient disk space (~20GB+ for the model and container)

## Installation

### Install Required Python Packages

```bash
pip install jupyter requests
```

### Verify Docker GPU Support

```bash
docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi
```

## Getting Started

1. **Obtain your NGC API Key**
   - Visit https://build.nvidia.com/nvidia/nvidia-nemotron-nano-9b-v2/deploy
   - Sign up or log in to NVIDIA NGC
   - Generate an API key

2. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook nemotron_nano_setup.ipynb
   ```

3. **Follow the notebook steps**
   - The notebook will guide you through:
     - Entering your API key
     - Logging into NVIDIA Container Registry
     - Pulling the NIM container
     - Running the container
     - Performing inference

## What the Notebook Does

The notebook automates the following workflow:

1. **API Key Setup** - Securely prompts for your NGC API key
2. **Docker Login** - Authenticates with NVIDIA Container Registry (nvcr.io)
3. **Container Pull** - Downloads the Nemotron Nano 9B v2 NIM image
4. **Container Run** - Starts the container with GPU support on port 8000
5. **Health Check** - Waits for the model to load and become ready
6. **Inference** - Demonstrates making inference calls to the model
7. **Custom Queries** - Provides a helper function for your own questions
8. **Cleanup** - Optionally stops the container when done

## Container Details

The NIM container runs with the following configuration:

- **Port**: 8000 (mapped to localhost:8000)
- **GPU**: All available GPUs
- **Shared Memory**: 16GB
- **Cache Directory**: `~/.cache/nim`
- **API Endpoint**: `http://localhost:8000/v1/chat/completions`

## Troubleshooting

### Container fails to start
- Check that Docker has GPU access: `docker run --rm --gpus all nvidia/cuda:11.8.0-base-ubuntu22.04 nvidia-smi`
- Ensure you have sufficient disk space
- Check Docker logs: `docker logs <container_id>`

### Service not ready
- The model takes 2-5 minutes to load initially
- Check container logs for any errors
- Verify port 8000 is not already in use: `lsof -i :8000`

### API key issues
- Ensure you're using a valid NGC API key
- Check that the key has access to the Nemotron Nano model

## Stopping the Container

Run the cleanup cell in the notebook, or manually stop via:

```bash
docker ps  # Find the container ID
docker stop <container_id>
```

## Model Information

- **Model**: NVIDIA Nemotron Nano 9B v2
- **Size**: ~9 billion parameters
- **Type**: Chat/Instruction model
- **API Format**: OpenAI-compatible chat completions

## Resources

- [NVIDIA NIM Documentation](https://docs.nvidia.com/nim/)
- [Nemotron Model Page](https://build.nvidia.com/nvidia/nvidia-nemotron-nano-9b-v2)
- [NGC Catalog](https://catalog.ngc.nvidia.com/)

## License

Please refer to NVIDIA's terms of service for the Nemotron model and NIM containers.

