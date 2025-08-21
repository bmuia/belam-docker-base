# Python Base Docker Image

A reusable Python 3.10 slim-based Docker image for microservices, preconfigured with common development tools, Python packages, and GitHub integration. Designed for fast builds, consistent environments, and automated CI/CD.

## Features

* Python 3.10-slim
* Essential build tools: `build-essential`, `libpq-dev`
* Python packaging tools: `pip`, `setuptools`, `wheel`
* Useful developer utilities: `vim`, `nano`, `less`, `curl`, `wget`, `git`, `iputils-ping`, `netcat`
* GitHub CLI installed for GitHub workflows
* Pre-created `/app/logs` directory
* Ready for production or development environments

## Usage

### Pull the image

```bash
docker pull belam443/python-base:latest
```

Or a specific version tag:

```bash
docker pull belam443/python-base:3.10
```

### Use as a base image in your Dockerfile

```dockerfile
FROM belam443/python-base:latest

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000
CMD ["python", "app.py"]
```

## Development

### Pre-commit hooks

You can set up pre-commit hooks for code formatting and checks:

```bash
pip install pre-commit
pre-commit install
```

### GitHub Workflows

This repository includes a GitHub Actions workflow (`.github/workflows/build-and-push.yml`) that automatically:

1. Builds the Docker image
2. Tags it with the Git tag or commit SHA
3. Pushes it to Docker Hub

Secrets required in GitHub:

* `DOCKER_USERNAME`
* `DOCKER_PASSWORD`

## Tags

* `latest` → always points to the latest build on `main`
* `3.10` → Python version tag
* `v*` → versioned images based on Git tags
* `sha-*` → commit SHA images for traceability

## Contributing

1. Fork the repository
2. Make your changes
3. Submit a pull request
4. CI/CD will automatically build and push updated images

## License

MIT License
