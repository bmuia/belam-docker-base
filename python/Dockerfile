FROM python:3.10-slim

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Install OS tools + dev tools + GitHub CLI
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    curl wget git \
    iputils-ping netcat-traditional \
    vim nano less \
    unzip \
    gnupg \
    && curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt-get update && apt-get install -y gh \
    && rm -rf /var/lib/apt/lists/*

# Optional logs folder
RUN mkdir -p /app/logs

# Expose common ports for app + Jupyter
EXPOSE 8000 8888

# Install Python packaging tools
RUN pip install --upgrade pip setuptools wheel

# Default command just keeps container alive
CMD ["python"]
