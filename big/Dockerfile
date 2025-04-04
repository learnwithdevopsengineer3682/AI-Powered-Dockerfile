# Large base image
FROM ubuntu:latest  

# Install dependencies
RUN apt-get update && apt-get install -y python3 python3-pip  

# Copy files
COPY app.py /app.py  
COPY requirements.txt /requirements.txt  

# Install Python dependencies
RUN pip3 install -r requirements.txt  

# Expose port
EXPOSE 5000  

CMD ["python3", "app.py"]
