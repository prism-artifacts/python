FROM bitnami/python:3.11

RUN install_packages poppler-utils tesseract-ocr antiword \
    && curl -sSL https://pdm-project.org/install-pdm.py | python3 -

# Add pdm to PATH using RUN
RUN echo 'export PATH="$PATH:$HOME/.local/bin"' >> /etc/bash.bashrc

WORKDIR /app

CMD [ "python" ]
