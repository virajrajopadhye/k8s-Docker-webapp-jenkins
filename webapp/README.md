# webapp
This is the backend for the web application developed for CSYE 7125 course. We have used node.js and express.js to create REST API endpoints for the application. We are using MySql for the database.
## Team Information

| Name | NEU ID | Email Address |
| --- | --- | --- |
| Viraj Rajopadhye| 001373609 | rajopadhye.v@northeastern.edu |
| Pranali Ninawe | 001377887 | ninawe.p@northeastern.edu |
| Harsha vardhanram kalyanaraman | 001472407 | kalyanaraman.ha@northeastern.edu | 

In order to run the application, navigate to the webapp folder install dependencies "npm install" and run "npm start".

Jenkins is setup to push docker images to docker hub. The images are tagged with both git commit number and latest tag.

The latest image can be pulled and run locally.

if running the application locally, create a .env file at the root of the project with the following variables

```bash
DB_USERNAME =<username>
DB_HOST =<hostname>
DB_NAME =<Database Name>
DB_PASS =<Database password>
```

# Run Docker image
```bash
docker run --network=host -p 3000:3000 <DockerHubID>/webapp:latest 
```

# Jenkins setup
1. A private repository should be created at Dockerhub
2. Commit to a webapp branch will trigger a pipeline to build and push the image to that private repository test

# Demo
1. A private repository should be created at Dockerhub.
2. Commit to a webapp branch will trigger a pipeline to build and push the image to that private repository

