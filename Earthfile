VERSION 0.7  
FROM python:3.9-slim  

deps:  
    # Copy dependency files  
    COPY requirements.txt ./
    
    # Install dependencies  
    RUN pip install -r requirements.txt
    
    # Save the installed dependencies  
    SAVE ARTIFACT /usr/local/lib/python3.9/site-packages site-packages

test:  
    FROM +deps  

    # Copy source code and tests  
    COPY . .  
    
    # Copy saved dependencies  
    #COPY +deps/site-packages /usr/local/lib/python3.11/site-packages  
    
    # Run pytest  
    RUN python -m pytest tests/  

build:  
    FROM +deps  
    
    # Copy the application code  
    COPY . .  
    
    # Copy saved dependencies  
    COPY +deps/site-packages /usr/local/lib/python3.11/site-packages  
    
    # Create a clean installation for production  
    RUN pip install --no-deps .  
    
    # Set the entry point  
    ENTRYPOINT ["python", "-m", "your_package_name"]  
    
    # Save the final image  
    SAVE IMAGE your-project:latest  

all:  
    BUILD +test  
    BUILD +build
