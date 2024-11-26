FROM python:3.9-slim  
WORKDIR /app
# Copy the requirements file into the container
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the app directory into the container
COPY src/ ./app/
EXPOSE 5000
CMD ["python", "-m", "app.main"]
