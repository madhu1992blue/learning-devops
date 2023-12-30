# DevOps and Kubernetes

## What is DevOps?

Automating portions of **Development** and **Operations** to shorten Product Development Lifecycle.  

- Development means to build a software.
- Operations involve setting up of service, scaling the HW/SW resources for a service, Termination of Service, Monitoring of service


## Why DevOps?

### Compete (Fastest team to get the following working will present)

1. Build a Fast API based web application  
   https://fastapi.tiangolo.com/#requirements
1. Write down the steps and share it with your friends so that they can develop.
   Document:
   1. Operating System
   1. Python Version
   1. Thirdparty Dependencies
1. Some thinking (Optionally document)
   1. How can we launch multiple replicas of the application?
   1. How can we restrict resources for the application?
  

### Let's automate Development Setup

#### File Contents

1. src/main.py
   ```
   from typing import Union
   import socket
   from fastapi import FastAPI
   
   app = FastAPI()
   
   @app.get("/")
   async def read_root():
   	return { "hostname": socket.gethostname() }
   ```

1. requirements.txt
   ```
   fastapi==0.108.0
   uvicorn[standard]==0.25.0
   ```

1. Dockerfile
   ```
   FROM "ubuntu:20.04"
    
   RUN apt-get update -y
   RUN apt-get install -y python3 python3-pip
    
   COPY requirements.txt requirements.txt
    
   # Install the packages
   RUN python3 -m pip install -r requirements.txt
    
   COPY src /opt/app
    
   WORKDIR /opt/app
    
   CMD [ "uvicorn" , "--host", "0.0.0.0", "main:app" ]
   ```

#### Build my first image

1. `docker build -t "my-first-image:0.1.0" .`

#### Run a container of the image

1. `docker run --rm -p 8000:8000 --name my-first-container my-first-image:0.1.0`

#### Visit the web application in browser

- localhost:8000








