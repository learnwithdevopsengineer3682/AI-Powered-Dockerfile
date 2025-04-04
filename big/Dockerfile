# Start from the latest Ubuntu image
FROM ubuntu:latest

# Install additional unnecessary packages to bloat the image
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    git \
    curl \
    vim \
    build-essential \
    libssl-dev \
    libffi-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    unzip \
    wget \
    libjpeg-dev \
    libmysqlclient-dev \
    python3-dev \
    && apt-get clean

# Install Node.js and npm to add bloat
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get install -y nodejs

# Install a few unnecessary global npm packages
RUN npm install -g lodash moment express

# Copy application and requirements files
COPY app.py /app.py
COPY requirements.txt /requirements.txt

# Install Python dependencies and unnecessary extra tools
RUN pip3 install --no-cache-dir --break-system-packages -r requirements.txt && \
    pip3 install --no-cache-dir flask requests numpy pandas && \
    pip3 install matplotlib seaborn scikit-learn

# Create extra directories (unnecessary)
RUN mkdir /data && mkdir /logs && mkdir /temp

# Install some system utilities and extra libraries to bloat the image
RUN apt-get install -y \
    sudo \
    less \
    tmux \
    htop \
    strace

# Expose unnecessary ports to further bloat the setup
EXPOSE 5000 8080 9090

# Set the working directory (unnecessary complexity)
WORKDIR /app

# Start unnecessary background services that are not required
RUN apt-get install -y apache2 && \
    service apache2 start

# Command to run the Python application (adding unnecessary complexity)
CMD ["bash", "-c", "python3 app.py && tail -f /dev/null"]
