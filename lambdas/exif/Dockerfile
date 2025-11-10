FROM public.ecr.aws/lambda/python:3.13

# Install uv (fast package installer)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Set working directory
WORKDIR /var/task

# Copy application code
COPY . .

# Use uv to install dependencies (fast, isolated)
# You can use requirements.txt or pyproject.toml
RUN if [ -f requirements.txt ]; then uv pip install -r requirements.txt --system; fi

# If you want to pin specific packages, uncomment and adjust below:
# RUN uv pip install pillow boto3 --system

# Set the command to your handler function
# Format: "<module>.<function>" — e.g., file named `lambda_function.py` and function `exif_handler`
CMD ["lambda_function.exif_handler"]