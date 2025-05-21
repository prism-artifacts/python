# --- Stage 1: Builder ---
    FROM python:3.12-slim AS builder

    WORKDIR /opt/app
    
    # Install build tools
    RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential gcc libffi-dev libpq-dev libssl-dev \
        && apt-get clean && rm -rf /var/lib/apt/lists/*
    
    # Install Python deps into /install directory
    COPY requirements.txt .
    RUN pip install --upgrade pip setuptools wheel
    RUN pip install --prefix=/install --no-cache-dir -r requirements.txt
    
    
    # --- Stage 2: Runtime ---
    FROM python:3.12-slim AS runtime
    
    WORKDIR /opt/app
    
    # Install only runtime system deps
    RUN apt-get update && apt-get install -y --no-install-recommends \
        libpq-dev libssl-dev libffi-dev libreoffice \
        && apt-get clean && rm -rf /var/lib/apt/lists/*
    
    # Copy installed Python packages from builder
    COPY --from=builder /install /usr/local
    
    # Download spaCy model (since spacy is now available in /usr/local)
    # RUN python -m spacy download en_core_web_lg
    
    # Copy app code if needed
    # COPY . .
    
    CMD ["python"]
    
