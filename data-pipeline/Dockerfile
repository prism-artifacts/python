# --- Stage 1: Builder ---
    FROM python:3.12-slim AS builder

    WORKDIR /opt/app
    
    # Install build tools for compiling wheels
    RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        gcc \
        libffi-dev \
        libpq-dev \
        libssl-dev \
        && apt-get clean && rm -rf /var/lib/apt/lists/*
    
    # Upgrade pip & install Python dependencies into /install
    COPY requirements.txt .
    RUN pip install --upgrade pip setuptools wheel
    RUN pip install --prefix=/install --no-cache-dir -r requirements.txt
    
    # Download and link spaCy model (medium size to save space)
    RUN python -m spacy download en_core_web_md && \
        python -m spacy link en_core_web_md en_core_web_md

    
    # --- Stage 2: Runtime ---
    FROM python:3.12-slim AS runtime
    
    WORKDIR /opt/app
    
    # Install only runtime system dependencies
    RUN apt-get update && apt-get install -y --no-install-recommends \
        libpq-dev \
        libssl-dev \
        libffi-dev \
        libreoffice \
        && apt-get clean && rm -rf /var/lib/apt/lists/*
    
    # Copy Python packages from builder stage
    COPY --from=builder /install /usr/local
    
    # Copy your app code (adjust this as needed)
    # COPY . .
    
    # Default command (adjust as needed)
    CMD ["python"]
    