FROM public.ecr.aws/lambda/python:3.13

# install uv (Python package manager)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# Set working directory
WORKDIR ${LAMBDA_TASK_ROOT}

# Copy dependency file if exists
COPY pyproject.toml ./

RUN uv sync --no-install-project --no-editable

COPY handler.py ./

RUN uv sync --no-editable

# set PYTHONPATH to include the virtual environment site-packages
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages"

# Set Lambda handler (filename.function_name)
CMD ["handler.exif_handler"]