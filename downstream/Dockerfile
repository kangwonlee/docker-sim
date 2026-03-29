# Downstream repo simulation (like eca-pytest-030)
# Build with: docker build --build-arg BASE=sim-n -t ds-n .

ARG BASE=sim-nsmpt

FROM ${BASE}

USER root

COPY pyproject.toml /app/pyproject.toml
RUN uv pip install --no-cache-dir --system /app/

USER runner
WORKDIR /tests/
RUN mkdir -p /tests/
COPY tests/* /tests/

RUN python3 -c "import pytest; import glob; \
    files = glob.glob('/tests/test_*.py'); \
    print('Found', len(files), 'files:', files); \
    assert files, 'No files in /tests/!'"

WORKDIR /app/
