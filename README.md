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
                
        docker build -t pysecond .
3 - Create a repo in dockerhub 
     12bk/pyapp
# Create a tag 
  docker tag pysecond 12bk/pyapp
   docker push 12bk/pyapp
4 -Create a ConfigMap
                
        apiVersion: v1
        kind: ConfigMap
        metadata:
          name: myapp
        data:
          DB_USER: your_db_user
          DB_PASSWORD: your_db_password
          DB_NAME: your_db_name
          DB_HOST: your_db_host
          DB_PORT: "your_db_port"
  5 -Deploy your Flask application
                
                apiVersion: apps/v1
                kind: Deployment
                metadata:
                  name: flask-app
                spec:
                  replicas: 1
                  selector:
                    matchLabels:
                      app: flask-app
                  template:
                    metadata:
                      labels:
                        app: flask-app
                    spec:
                      containers:
                        - name: flask-app
                          image: 12bk/pyapp
                          ports:
                            - containerPort: 5000
                          envFrom:
                            - configMapRef:
                                name: myapp

          
   
