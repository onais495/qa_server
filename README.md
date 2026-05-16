#QA Server

##DevOps Setup

###Running the Stack Locally

Run docker compose up --build -d

###URL to Test

Once the images are built and the containers are running (test this using docker ps),
the tests will be run on port 80. The port doesn't need to be specified in the URL since it is defaulted to HTTP port which is 80.
test the frontend with http://localhost
and the backend with http://localhost/api/ping

###Services
frontend: React + Vite application served by Nginx
backend: .NET 10 REST API handling backend logic 
nginx: Reverse proxy responsible for routing traffic to frontend and backend

###CI/CD pipeline

The full pipeline is defined in '.github/workflows/deploy-qa.yml' and is set to trigger automatically everytime there is a push
to the main branch
What the pipeline will do:
Builds the docker images for frontend, backend and nginx
pushes the images to docker hub tagged with the git commit SHA
SSHs into the QA server and pulls the latest images
Runs docker compose up -d to deploy the updated containers
