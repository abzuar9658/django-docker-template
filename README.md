# Django Docker Template

A modern, production-ready Docker template for Django projects based on Python 3.12 and Debian Bookworm.

## Features

- Multi-stage Docker build for optimized image size
- Python 3.12 with slim-bookworm base image
- Efficient dependency caching with wheels
- Proper user permissions (runs as non-root)
- Pre-configured for Django static files
- Development-ready with essential tools

## Project Structure

```
django-docker-template/
├── Dockerfile                      # Multi-stage Docker configuration
├── docker-compose.yml              # Docker Compose configuration
├── requirements/                   # Python dependencies
│   ├── base.txt                    # Base dependencies
│   ├── local.txt                   # Development dependencies
│   └── production.txt              # Production dependencies
└── docker/
    └── local/
        └── django/
            ├── entrypoint.sh       # Container entrypoint script
            └── start.sh            # Django startup script
```

## Getting Started

### Prerequisites

- Docker and Docker Compose
- Git

### Setup Instructions

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/django-docker-template.git
   cd django-docker-template
   ```

2. Create your Django project or copy an existing one into this directory

3. Create the necessary requirements files:
   ```bash
   mkdir -p requirements
   ```
   
   Create `requirements/base.txt` with your core dependencies:
   ```
   django>=5.0.0
   psycopg2>=2.9.9
   ```
   
   Create `requirements/local.txt`:
   ```
   -r base.txt
   django-debug-toolbar>=4.2.0
   ```
   
   Create `requirements/production.txt`:
   ```
   -r base.txt
   gunicorn>=21.0.0
   ```

4. Set up the Docker scripts:
   ```bash
   mkdir -p docker/local/django
   ```
   
   Create the entrypoint script at `docker/local/django/entrypoint.sh`:
   ```bash
   # See the entrypoint.sh.example file for a template
   # This script waits for the database to be ready
   ```
   
   Create the start script at `docker/local/django/start.sh`:
   ```bash
   # See the start.sh.example file for a template
   # This script runs migrations and starts the development server
   ```
   
   Make the scripts executable:
   ```bash
   chmod +x docker/local/django/entrypoint.sh docker/local/django/start.sh
   ```

5. Create a docker-compose.yml file:
   ```bash
   # See docker-compose.example.yml for a template
   ```

6. Build and run the container:
   ```bash
   docker compose build
   docker compose up
   ```

## Customization

### Changing the Python Version

Update the first line in the Dockerfile:
```dockerfile
FROM docker.io/python:3.12.2-slim-bookworm AS python
```

### Changing Build Environment

The template supports different build environments through the `BUILD_ENVIRONMENT` argument:

```bash
docker build --build-arg BUILD_ENVIRONMENT=production -t myapp .
```

### Adding Custom Dependencies

Modify the respective requirements file in the `requirements/` directory.

## Common Issues

- Windows users may need to ensure line endings are set to LF for shell scripts
- If you encounter permission issues, check the ownership of mounted volumes
- The error `api-get: command not found` in the Dockerfile should be fixed to `apt-get`

## License

[MIT License](LICENSE)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
