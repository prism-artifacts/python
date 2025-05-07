FROM python:3.12-slim AS builder

WORKDIR /opt/app

# Install system dependencies needed only for building wheels
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gcc \
    libffi-dev \
    libpq-dev \
    libssl-dev \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install pip and wheel tools
RUN pip install --upgrade pip setuptools wheel

# Copy only the requirements to install deps (cache layer)
COPY requirements.txt .

# Install Python dependencies into a target directory
RUN pip install -r requirements.txt

WORKDIR /opt/app

# Install runtime-only system packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq-dev \
    libssl-dev \
    libffi-dev \
    libreoffice \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy installed Python packages from builder

# Download spaCy model (only if really needed)
RUN python -m spacy download en_core_web_lg