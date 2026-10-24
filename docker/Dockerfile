FROM debian:trixie-slim

WORKDIR /content

COPY ./pyproject.toml ./
COPY ./uv.lock ./
COPY ./.python-version ./
COPY ./apt.txt ./

ENV VIRTUAL_ENV=/opt/venvs/handson-mlp
ENV UV_PATH=/root/.local/bin
ENV PATH="$UV_PATH:$VIRTUAL_ENV/bin:$PATH"

# Choose the PyTorch variants, such as cpu or cu126
# See the list at https://pytorch.org/get-started/locally/ (select Linux)
ARG PT_VARIANT=cpu
ARG WITH_BOX2D=false
ENV PT_VARIANT=${PT_VARIANT}

RUN apt-get update && \
    xargs -a apt.txt apt-get install -y --no-install-recommends && \
    curl -LsSf https://astral.sh/uv/install.sh | sh && \
    uv venv $VIRTUAL_ENV && \
    if [ "$WITH_BOX2D" = "true" ]; then \
        uv sync --active --frozen --extra box2d; \
    else \
        uv sync --active --frozen; \
    fi && \
    \
    if [ "$PT_VARIANT" != "cpu" ]; then \
        echo "PyTorch Variant = ${PT_VARIANT}" && \
        uv pip install --torch-backend "$PT_VARIANT" \
            --reinstall-package torch --reinstall-package torchvision --reinstall-package torchaudio \
            "torch>=2.8.0,<3.0.0" "torchvision>=0.23.0,<0.27.0" "torchaudio>=2.8.0,<3.0.0"; \
    fi && \
    apt-get purge -y build-essential cmake && \
    apt-get autoremove -y && \
    uv cache clean && \
    rm -rf /var/lib/apt/lists/* && \
    echo 'Success'

EXPOSE 8888

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]

