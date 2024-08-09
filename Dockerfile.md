# Dockerfile Documentation
## Define Example Dockerfile
```dockerfile
FROM <source_image>
RUN <command>
WORKDIR <path>
COPY <path_on_host> <path_on_guest>
```
## Create Virtual Python Environment With Multi Stage Build
```dockerfile
FROM python:<version1> AS builder
WORKDIR <path1>
RUN python -m venv </path/to/new/venv>
ENV PATH="<path>/</path/to/new/venv>/bin:$PATH"
COPY <source> requirements.txt
RUN pip install -r requirements.txt
FROM python:<version1>
WORKDIR <path1>
COPY --from=builder </path/to/new/venv> </path/to/new/venv>
ENV PATH="<path>/</path/to/new/venv>/bin:$PATH"
COPY <path_on_host> <path_on_guest>
CMD ["python app.py"]
```