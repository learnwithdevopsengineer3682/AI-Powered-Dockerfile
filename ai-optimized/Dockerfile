# Smaller base image
FROM python:3.9-slim-buster

# Set work directory
WORKDIR /app

# Copy requirements first to optimize caching
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application files
COPY . .

# Expose port 5000 for the application
EXPOSE 5000

# Run the application when container starts
CMD ["python", "app.py"]
