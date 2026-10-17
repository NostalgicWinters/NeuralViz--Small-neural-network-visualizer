# Set Base image
FROM python:3.14

# Set the working directory
WORKDIR /backend

# Copy requirements
COPY ./requirements.txt /backend/requirements.txt

# Pip install
RUN pip install --no-cache-dir --upgrade -r ./requirements.txt

# Copy the actual app
COPY ./ /backend

# Run container
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
