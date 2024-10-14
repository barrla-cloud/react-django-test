# Use the official Python 3.10.12-slim image
FROM python:3.10.12-slim

# Set environment variables to avoid .pyc files and buffer issues
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install system dependencies, including MariaDB client (compatible with MySQL)
RUN apt-get update && apt-get install -y \
    mariadb-client \
    build-essential \
    libmariadb-dev \
    pkg-config \
    gcc \
    python3-dev \
    && apt-get clean

# Set the working directory
WORKDIR /app

# Copy the requirements file into the container
COPY requirements.txt /app/

# Install Python dependencies
RUN pip install --upgrade pip && pip install -r requirements.txt

# Copy the entire project into the container
COPY . /app/

# Collect static files
RUN python manage.py collectstatic --noinput

# Expose the Django app's port (typically 8000)
EXPOSE 8000

# Command to run the Django app using Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "blog.wsgi:application"]
