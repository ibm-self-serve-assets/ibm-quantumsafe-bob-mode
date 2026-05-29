
# Python MCP Server
FROM python:3.12-slim
 
# Set working directory
WORKDIR /app
 
# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc curl \
    && rm -rf /var/lib/apt/lists/*
 
# Copy and install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
 
# Copy application source
COPY . .
 
# Create /data directory and set permissions
RUN mkdir -p /data && chmod 755 /data
 
# Expose SSE port
EXPOSE 8002
 
# Run the MCP server with SSE transport
ENTRYPOINT ["python", "server.py", "--transport", "sse"]