FROM bitnami/python:3.11

RUN install_packages libxml2-dev libxslt1-dev antiword \
    unrtf poppler-utils tesseract-ocr \
    flac ffmpeg lame libmad0 libsox-fmt-mp3 \
    sox libjpeg-dev swig \
    && curl -sSL https://pdm-project.org/install-pdm.py | python3 -

# Add pdm to PATH using RUN
RUN echo 'export PATH="$PATH:$HOME/.local/bin"' >> /etc/bash.bashrc

WORKDIR /app

CMD [ "python" ]
