# Stage 1: Build dependencies
FROM python:3.13.5-slim AS builder

WORKDIR /app

# Install build dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc

COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# Stage 2: Minimal runtime image
FROM python:3.13.5-slim

WORKDIR /app

# Install runtime deps
RUN apt-get update && \
    apt-get install -y --no-install-recommends sqlite3 libsqlite3-dev && \
    rm -rf /var/lib/apt/lists/*

# Copy python dependencies from builder
COPY --from=builder /root/.local /root/.local
ENV PATH=/root/.local/bin:$PATH

# Copy the application code
COPY . .

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

