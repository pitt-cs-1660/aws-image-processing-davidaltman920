FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

############
# Install dependencies and configure Lambda runtime
############

# Set working directory to AWS Lambda task root
WORKDIR ${LAMBDA_TASK_ROOT}

# Copy dependency file (if exists) and code
# If you don’t have requirements.txt, you can skip this copy
COPY requirements.txt ./

# Install dependencies using uv (fast Python package manager)
# Pillow = image library, boto3 = AWS SDK
RUN if [ -f requirements.txt ]; then \
        uv pip install --no-cache-dir -r requirements.txt; \
    else \
        uv pip install --no-cache-dir pillow boto3; \
    fi

# Copy the rest of your application code
COPY . .

# Set the Lambda handler (module.function_name)
# Assuming your Python file is named greyscale_handler.py
CMD ["greyscale_handler.greyscale_handler"]
