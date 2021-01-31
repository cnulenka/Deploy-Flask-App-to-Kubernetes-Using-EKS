# Deploying a Flask API

Containerize and deploy a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

The Flask app consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

The app relies on a secret set as the environment variable `JWT_SECRET` to produce a JWT. The built-in Flask server is adequate for local development, but not production, so  the production-ready [Gunicorn](https://gunicorn.org/) server is used to deploy the app.

## Dependencies

- Docker Engine
    - Installation instructions for all OSes can be found [here](https://docs.docker.com/install/).
 - AWS Account
     - You can create an AWS account by signing up [here](https://aws.amazon.com/#).
     
## Project Steps

1. Write a Dockerfile for this Flask API
2. Build and test the container locally
3. Create an EKS cluster
4. Store a secret using AWS Parameter Store
5. Create a CodePipeline pipeline triggered by GitHub checkins
6. Create a CodeBuild stage which will build, test, and deploy your code
