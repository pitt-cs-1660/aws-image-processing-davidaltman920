FROM public.ecr.aws/lambda/python:3.13

# install uv (Python package manager)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Set working directory
WORKDIR ${LAMBDA_TASK_ROOT}

# Copy dependency file if exists
COPY requirements.txt ./

# Use uv to install dependencies (fast & layer-cached)
RUN if [ -f requirements.txt ]; then \
        uv pip install --system --no-cache -r requirements.txt; \
    else \
        uv pip install --system --no-cache pillow boto3; \
    fi

# Copy all Lambda function code
COPY . .

# Set Lambda handler (filename.function_name)
CMD ["resize_handler.resize_handler"]