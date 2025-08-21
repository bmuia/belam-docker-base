FROM python:3.10-slim

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Install OS + dev tools + GitHub CLI
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    curl wget git \
    iputils-ping netcat-traditional \
    vim nano less \
    unzip \
    # GitHub CLI
    && curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | tee /etc/apt/sources.list.d/github-cli.list > /dev/null \
    && apt-get update && apt-get install -y gh \
    && rm -rf /var/lib/apt/lists/*


COPY requirements.txt .

# Install Python deps + dev tools
RUN pip install --upgrade pip setuptools wheel \
    && pip install --no-cache-dir -r requirements.txt \
    && pip install --no-cache-dir \
        gunicorn \
        pytest \
        black \
        ipython \
        httpie \
        ipdb \
        jupyter \
        pre-commit \
        flake8 \
        isort

# Add logs folder
RUN mkdir -p /app/logs

# Expose ports for app + Jupyter
EXPOSE 8000 8888

# Default CMD
CMD ["python"]
