# 1. Add a base image (a lightweight Python environment)
FROM python:3.12.0-slim-bookworm

# Set environment variables to make Python run better inside Docker
ENV PYTHONBUFFERED 1
ENV PYTHONWRITEBYTECODE 1

# Set the working directory inside the container
ENV APP=/app
WORKDIR $APP

# 2. Add the requirements.txt file and install dependencies
COPY requirements.txt $APP
RUN pip3 install -r requirements.txt

# 3. Copy the rest of your Django project code into the container
COPY . $APP

# 4. Expose the port the app will run on
EXPOSE 8000

# 5. Make the entrypoint script executable (we will create this file next)
RUN chmod +x /app/entrypoint.sh

# 6. Set the entrypoint script to run when the container starts
ENTRYPOINT ["/bin/bash","/app/entrypoint.sh"]

# 7. Define the default command to run the application using Gunicorn
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]