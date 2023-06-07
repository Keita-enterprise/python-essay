1 - Write Dockerfile 
# Use the official Python base image
        FROM python:3.9

        # Set the working directory inside the container
        WORKDIR /app

        # Copy the requirements file to the working directory
        COPY requirements.txt .

        # Install the Python dependencies
        RUN pip install -r requirements.txt

        # Copy the application code to the working directory
        COPY . .

        # Expose the port on which the Flask app will run
        EXPOSE 5000

        # Set the command to run the Flask application
        CMD ["python", "app.py"]
        
2 - Build the docker image 
                
        docker build -t pysecond2 .
2 - Build the docker image 
                
        docker build -t pysecond2 .

