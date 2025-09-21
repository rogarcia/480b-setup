# Qwen3-Coder-480B-A35B-Instruct Comprehensive API Reference

## Overview

This document provides comprehensive documentation for all public APIs, functions, and components in the Qwen3-Coder-480B-A35B-Instruct setup system. The system includes web components, Python APIs, installation scripts, and Docker configuration.

## Table of Contents

1. [Project Configuration](#project-configuration)
2. [Web Components](#web-components)
3. [Python APIs](#python-apis)
4. [Installation Scripts](#installation-scripts)
5. [Docker Configuration](#docker-configuration)
6. [Usage Examples](#usage-examples)
7. [Performance Guidelines](#performance-guidelines)

---

## Project Configuration

### package.json

The main configuration file for the Next.js web application.

**Location**: `/web/package.json`

**Properties**:

| Property | Type | Description | Required |
|----------|------|-------------|----------|
| `name` | string | Project name | ✓ |
| `version` | string | Version number | ✓ |
| `private` | boolean | Private repository flag | ✓ |
| `scripts` | object | Available npm scripts | ✓ |
| `dependencies` | object | Runtime dependencies | ✓ |
| `devDependencies` | object | Development dependencies | ✓ |

**Available Scripts**:

```bash
# Development server
npm run dev

# Production build
npm run build

# Start production server
npm start

# Lint code
npm run lint
```

**Dependencies**:

| Package | Version | Purpose |
|---------|---------|---------|
| `react` | 18.2.0 | Core React framework |
| `react-dom` | 18.2.0 | React DOM renderer |
| `next` | 14.2.5 | Next.js framework |

**Development Dependencies**:

| Package | Version | Purpose |
|---------|---------|---------|
| `typescript` | ^5 | TypeScript compiler |
| `tailwindcss` | ^3.4.0 | CSS framework |
| `eslint` | ^8 | JavaScript linting |

### requirements.txt

Python dependencies for the model inference environment.

**Location**: `/config/requirements.txt`

**Core Dependencies**:

| Package | Version | Purpose |
|---------|---------|---------|
| `torch` | 2.3.0 | PyTorch ML framework |
| `transformers` | 4.54.1 | Hugging Face transformers |
| `accelerate` | 0.33.0 | Model acceleration |
| `tokenizers` | 0.19.1 | Text tokenization |
| `peft` | 0.12.0 | Parameter-efficient fine-tuning |
| `bitsandbytes` | 0.43.3 | Memory optimization |

**Usage**:

```bash
# Install all dependencies
pip install -r config/requirements.txt

# Install with CUDA support
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

---

## Web Components

### TerminalHeader

A terminal-style header component displaying system information.

**Location**: `/web/src/components/TerminalHeader.tsx`

**Props**:

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `currentTime` | string | ✓ | Current timestamp in ISO format |

**Example Usage**:

```tsx
import TerminalHeader from '@/components/TerminalHeader'

function App() {
  const currentTime = new Date().toISOString().slice(0, 19) + 'Z'

  return (
    <TerminalHeader currentTime={currentTime} />
  )
}
```

**Features**:
- Terminal-style window controls (red, yellow, green dots)
- System path display (`qwen-480b-setup@ubuntu:~/installation`)
- Real-time timestamp
- Terminal aesthetic styling

### QuickStart

Component providing quick installation instructions and methods.

**Location**: `/web/src/components/QuickStart.tsx`

**Features**:
- One-click installation command
- Installation method comparison
- Performance expectations display
- Copy-to-clipboard functionality
- GitHub repository links

**Commands Provided**:
- `curl -fsSL https://raw.githubusercontent.com/twobitapps/480b-setup/main/install.sh | bash`
- `./install.sh` (automated)
- `MANUAL_INSTALL.md` (manual)
- `docker-compose up` (Docker)

### SystemRequirements

Component displaying hardware and software requirements.

**Location**: `/web/src/components/SystemRequirements.tsx`

**Hardware Requirements**:

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| GPU | NVIDIA A100 80GB | NVIDIA H100 80GB HBM3 |
| RAM | 64GB system memory | 128GB+ system memory |
| Storage | 500GB free space | 1TB+ NVMe SSD |
| CPU | 16+ cores | 32+ cores (Xeon/EPYC) |

**Software Requirements**:
- Ubuntu 22.04 LTS (recommended)
- Ubuntu 20.04 LTS
- Python 3.8-3.11 (3.10 recommended)
- CUDA 12.1+ (auto-installed)
- Docker (optional)

**Verification Command**:
```bash
curl -fsSL https://raw.githubusercontent.com/twobitapps/480b-setup/main/scripts/system_check.sh | bash
```

### InstallationSteps

Step-by-step installation guide component.

**Location**: `/web/src/components/InstallationSteps.tsx`

**Installation Steps**:

| Step | Title | Time | Status |
|------|-------|------|--------|
| 1 | System Verification | ~30 seconds | Required |
| 2 | Download Installer | ~5 seconds | Required |
| 3 | Run Installation | 30-90 minutes | Required |
| 4 | Verify Installation | 2-5 minutes | Recommended |
| 5 | Performance Benchmark | 5-10 minutes | Optional |

**Commands**:
1. System check: `curl -fsSL https://raw.githubusercontent.com/twobitapps/480b-setup/main/scripts/system_check.sh | bash`
2. Download installer: `curl -fsSL https://raw.githubusercontent.com/twobitapps/480b-setup/main/install.sh -o install.sh && chmod +x install.sh`
3. Run installation: `./install.sh`
4. Verify: `source ~/activate_qwen480b.sh && python test_inference.py`
5. Benchmark: `python benchmark.py`

### Documentation

Component providing access to all documentation resources.

**Location**: `/web/src/components/Documentation.tsx`

**Documentation Files**:

| File | Type | Description |
|------|------|-------------|
| `README.md` | Guide | Main overview and quick start |
| `MANUAL_INSTALL.md` | Guide | Detailed installation instructions |
| `TROUBLESHOOTING.md` | Reference | Common issues and solutions |
| `install.sh` | Script | Main installation script |
| `system_check.sh` | Script | System requirements verification |
| `test_installation.sh` | Script | Installation testing |
| `basic_inference.py` | Example | Python inference example |
| `requirements.txt` | Config | Python dependencies |

### Footer

Footer component with links to resources and community.

**Location**: `/web/src/components/Footer.tsx`

**Links Provided**:
- GitHub Repository
- Troubleshooting Guide
- Download Releases
- Community Discussions
- Bug Reports
- Community Wiki
- Official Qwen Repository
- Hugging Face Model

---

## Python APIs

### QwenCodeGenerator

Main class for model inference and code generation.

**Location**: `/examples/basic_inference.py`

**Constructor**:

```python
QwenCodeGenerator(model_path=None, device="auto")
```

**Parameters**:
- `model_path` (str, optional): Path to model directory
- `device` (str): Device to run model on ("auto", "cuda", "cpu")

**Methods**:

#### load_model()

Loads the model and tokenizer from the specified path.

**Returns**: None

**Raises**:
- `ValueError`: If model path is not found
- `RuntimeError`: If model loading fails

**Example**:
```python
generator = QwenCodeGenerator()
generator.load_model()
```

#### generate_code()

Generates code based on the provided prompt.

**Parameters**:
- `prompt` (str): Input prompt text
- `max_tokens` (int, optional): Maximum tokens to generate (default: 200)
- `temperature` (float, optional): Sampling temperature (default: 0.7)
- `top_p` (float, optional): Top-p sampling parameter (default: 0.9)

**Returns**:
```python
{
    'prompt': str,              # Original prompt
    'generated_text': str,      # Generated code
    'full_response': str,       # Complete response
    'inference_time': float,    # Time taken (seconds)
    'tokens_generated': int,    # Number of tokens generated
    'tokens_per_second': float  # Generation speed
}
```

**Example**:
```python
result = generator.generate_code(
    "Write a Python function to sort a list:",
    max_tokens=150,
    temperature=0.7
)

print(f"Generated: {result['generated_text']}")
print(f"Speed: {result['tokens_per_second']:.1f} tokens/sec")
```

### Utility Functions

#### _get_default_model_path()

Internal method to get the default model path from environment variables.

**Returns**: str or None

**Environment Variables**:
- `INSTALL_DIR`: Installation directory path

---

## Installation Scripts

### install.sh

Main automated installation script.

**Location**: `/install.sh`

**Functions**:

#### check_root()

Verifies the script is not run as root user.

**Returns**: None

**Exit Codes**: 1 if run as root

#### check_system_requirements()

Validates system meets minimum requirements.

**Checks**:
- Ubuntu version (20.04+)
- Available disk space (500GB+)
- System memory (64GB+ recommended)
- NVIDIA GPU with sufficient memory (80GB+)

**Returns**: None

**Exit Codes**: 1 if requirements not met

#### install_system_dependencies()

Installs required system packages.

**Packages Installed**:
- build-essential, cmake
- curl, wget, git, git-lfs
- python3, python3-pip, python3-venv
- GPU monitoring tools (htop, nvtop)
- Development libraries

#### setup_cuda()

Installs and configures CUDA 12.1.

**Features**:
- Checks for existing CUDA installation
- Downloads and installs CUDA 12.1 if needed
- Updates PATH and LD_LIBRARY_PATH
- Verifies installation

#### create_python_environment()

Creates isolated Python virtual environment.

**Location**: `$HOME/qwen480b_env`

**Features**:
- Creates virtual environment
- Upgrades pip and setuptools
- Activates environment

#### install_python_dependencies()

Installs Python packages with specific versions.

**Key Packages**:
- PyTorch 2.3.0 with CUDA 12.1 support
- Transformers 4.54.1
- Model optimization libraries (PEFT, bitsandbytes)
- Performance monitoring tools

#### download_model()

Downloads the Qwen3-Coder-480B-A35B-Instruct model.

**Features**:
- Downloads from Hugging Face Hub
- Supports resume functionality
- Multiple retry attempts with exponential backoff
- Progress tracking
- Backup mirror servers

#### create_test_scripts()

Creates verification and testing scripts.

**Scripts Created**:
- `test_inference.py`: Basic functionality test
- `benchmark.py`: Performance benchmarking
- `activate_qwen480b.sh`: Environment activation

#### run_installation_test()

Runs comprehensive installation verification.

**Tests**:
- Model loading
- Basic inference
- GPU memory usage
- Performance metrics

**Usage**:
```bash
# Run main installation
./install.sh

# Verify installation
source ~/activate_qwen480b.sh
python test_inference.py
```

---

## Docker Configuration

### Dockerfile

Docker image configuration for containerized deployment.

**Location**: `/docker/Dockerfile`

**Base Image**: `nvidia/cuda:12.1-devel-ubuntu22.04`

**Features**:
- CUDA 12.1 development environment
- Python 3 virtual environment
- All required dependencies pre-installed
- Model directory structure
- Entry point script

**Environment Variables**:
- `INSTALL_DIR=/opt/qwen480b_env`
- `HF_HOME=/opt/qwen480b_env/huggingface_cache`
- `PATH` includes Python and CUDA binaries

### docker-compose.yml

Docker Compose configuration for complete deployment.

**Location**: `/docker/docker-compose.yml`

**Services**:
- Main application container
- Volume mounts for data persistence
- GPU passthrough configuration
- Network configuration

**Usage**:
```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs -f
```

### Entry Point Script

Container initialization script.

**Location**: `/docker/entrypoint.sh`

**Functions**:
- Environment setup
- Model download (if needed)
- Service initialization
- Health checks

---

## Usage Examples

### Basic Model Usage

```python
from transformers import AutoTokenizer, AutoModelForCausalLM
import torch

# Initialize model
model_path = "~/qwen480b_env/models/qwen3-coder-480b"
tokenizer = AutoTokenizer.from_pretrained(model_path, trust_remote_code=True)
model = AutoModelForCausalLM.from_pretrained(
    model_path,
    torch_dtype=torch.float16,
    device_map="auto",
    trust_remote_code=True,
)

# Generate code
prompt = "Write a Python function to calculate fibonacci numbers:"
inputs = tokenizer(prompt, return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=200)
response = tokenizer.decode(outputs[0], skip_special_tokens=True)

print(response)
```

### Performance Monitoring

```bash
# Monitor GPU usage
watch -n 1 nvidia-smi

# Run performance benchmark
python benchmark.py

# Check system resources
htop
gpustat -i 1
```

### Environment Management

```bash
# Activate environment
source ~/activate_qwen480b.sh

# Quick commands
python test_inference.py    # Test installation
python benchmark.py         # Performance test
nvidia-smi                  # Check GPU status
```

### Docker Usage

```bash
# Build and run container
docker build -t qwen480b docker/
docker run --gpus all -p 8000:8000 qwen480b

# Use docker-compose
docker-compose up -d
```

---

## Performance Guidelines

### Hardware Requirements

| Component | Minimum | Recommended | Optimal |
|-----------|---------|-------------|---------|
| GPU Memory | 80GB | 128GB | 256GB |
| System RAM | 64GB | 128GB | 256GB+ |
| Storage | 500GB SSD | 1TB NVMe | 2TB NVMe |
| CPU Cores | 16 | 32 | 64+ |

### Performance Tuning

#### GPU Memory Optimization

```python
# Use float16 for reduced memory usage
model = AutoModelForCausalLM.from_pretrained(
    model_path,
    torch_dtype=torch.float16,  # Half precision
    device_map="auto",          # Automatic device placement
    low_cpu_mem_usage=True,     # Memory optimization
)
```

#### Generation Parameters

```python
# Optimized generation parameters
outputs = model.generate(
    **inputs,
    max_new_tokens=200,         # Limit output length
    temperature=0.7,           # Balance creativity/safety
    top_p=0.9,                 # Nucleus sampling
    do_sample=True,            # Enable sampling
    pad_token_id=tokenizer.eos_token_id,
    repetition_penalty=1.1,    # Reduce repetition
)
```

#### Memory Management

```python
# Clear GPU cache after generation
torch.cuda.empty_cache()
import gc
gc.collect()
```

### Expected Performance

| Metric | H100 80GB | A100 80GB | Expected Range |
|--------|-----------|-----------|----------------|
| Model Loading | 2-3 min | 3-5 min | 2-5 minutes |
| First Inference | 10-15s | 15-20s | 10-20 seconds |
| Tokens/Second | 100-200 | 80-150 | 80-200 tok/s |
| GPU Memory | ~45-50GB | ~45-50GB | 45-50GB |

---

## Troubleshooting

### Common Issues

#### GPU Memory Errors

**Problem**: CUDA out of memory errors

**Solutions**:
1. Check available GPU memory: `nvidia-smi`
2. Use `torch_dtype=torch.float16` for half precision
3. Enable `low_cpu_mem_usage=True`
4. Clear cache between generations: `torch.cuda.empty_cache()`

#### Model Loading Failures

**Problem**: Model fails to load or download

**Solutions**:
1. Verify disk space: `df -h`
2. Check internet connectivity
3. Use backup mirrors in `install.sh`
4. Verify Hugging Face token if using private models

#### Installation Script Errors

**Problem**: Installation script fails

**Solutions**:
1. Check logs: `cat ~/qwen480b_install.log`
2. Verify system requirements: `./scripts/system_check.sh`
3. Run manual installation: `MANUAL_INSTALL.md`
4. Check network connectivity and disk space

### Getting Help

- **Issues**: [GitHub Issues](https://github.com/twobitapps/480b-setup/issues)
- **Discussions**: [GitHub Discussions](https://github.com/twobitapps/480b-setup/discussions)
- **Documentation**: [Project Wiki](https://github.com/twobitapps/480b-setup/wiki)

---

## Contributing

### Development Setup

```bash
# Clone repository
git clone https://github.com/twobitapps/480b-setup.git
cd 480b-setup

# Install dependencies
cd web
npm install

# Run development server
npm run dev
```

### Code Structure

```
480b-setup/
├── web/src/components/     # React components
├── examples/              # Python examples
├── scripts/               # Installation scripts
├── config/                # Configuration files
├── docker/                # Docker configuration
└── docs/                  # Documentation
```

### Testing

```bash
# Run Python tests
python -m pytest

# Run web application tests
npm test

# Lint code
npm run lint
```

---

## License

This project is licensed under the MIT License. See the main repository for full license text.

## Version History

- **v1.0.0**: Initial release with automated installation and web interface
- **v1.1.0**: Added Docker support and improved error handling
- **v1.2.0**: Enhanced performance monitoring and troubleshooting

---

*Last updated: September 21, 2025*