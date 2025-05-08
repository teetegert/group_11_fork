# Use the official PySpark Jupyter image as the base
FROM quay.io/jupyter/pyspark-notebook:spark-3.5.3

# Switch to root for installing additional packages
USER root

# Create a working directory
WORKDIR /home/jovyan

# Copy requirements.txt into container
COPY requirements.txt /tmp/requirements.txt

# Install Python packages using pip
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# Ensure permissions are correct for the jovyan user
RUN chown -R jovyan:users /home/jovyan

# Switch back to jovyan (non-root) for normal usage
USER jovyan
