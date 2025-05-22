# Stage 1: Build stage
FROM python:3.11-slim as builder

WORKDIR /app

# Install build dependencies if needed (e.g. gcc, build-essential)
RUN apt-get update && apt-get install -y build-essential && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /app/
RUN pip install --upgrade pip
RUN pip install --prefix=/install -r requirements.txt

COPY . /app/

# Stage 2: Final stage (smaller image)
FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Copy installed packages from builder stage
COPY --from=builder /install /usr/local

# Copy app code
COPY --from=builder /app /app

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
