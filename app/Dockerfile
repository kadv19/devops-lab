# Stage 1: Builder
FROM python:3.12-slim AS builder
WORKDIR /app
COPY requirements.txt .
# Install dependencies into a local folder
RUN pip install --user --no-cache-dir -r requirements.txt

# Stage 2: Final Runner
FROM python:3.12-slim
WORKDIR /app

# Copy only the installed dependencies from the builder
COPY --from=builder /root/.local /root/.local
# Copy the app code
COPY . .

# Update PATH to find the installed packages
ENV PATH=/root/.local/bin:$PATH

EXPOSE 5000
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]

