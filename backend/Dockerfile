# Use an official Python runtime as a parent image
FROM python:3.12-slim

# Set the working directory in the container
WORKDIR /app

# Install system dependencies
# - apt-get update: Refreshes the package index
# - apt-get install -y ...: Installs zbar libraries and tools without prompting
# - rm -rf /var/lib/apt/lists/*: Cleans up the apt cache to reduce image size
RUN apt-get update && apt-get install -y libzbar0 zbar-tools libzbar-dev && rm -rf /var/lib/apt/lists/*

# Copy the dependencies file to the working directory
COPY requirements.txt .

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application's code to the working directory
COPY . .

# The command to run the application
# Railway will inject the PORT environment variable. We default to 8000 for local use.
CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port $PORT"]
