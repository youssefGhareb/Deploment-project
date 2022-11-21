# Advanced Full Stack Web Development Project 3

This project is deploying a full stack web application with CI/CD using AWS and CircleCI

## App Dependencies

This full stack application was developed by Udacity, it uses :

1. Angular JS for the client side
2. Node JS and postgres SQL for the server side

## Infrastructure Description (AWS)

The project consists of:

1. A web API developed using node JS and Typescript, this API is hosted on Elastic Beanstalk on AWS
2. An Angular JS client side application, and this consists of static files hosted on a S3 bucket
3. A PostgresSQL relational database, hosted on a RDS psql instance.

## Pipeline Process (Circle CI)

This project makes use of a CircleCI pipeline for continous integration and deployment. 

Circle CI makes use of scripts provide in `package.json` files to perform a set of stes every time a change is commited to the Github repository containing the project files.

### Steps:

#### 1. Building the project:
   
   1.  Spin up enviroment: Circle CI configures a virtual enviroment to run the project.
   2.  Install Node JS: Circle CI installs the Node JS version specified in the `package.json` file.
   3.  Checkout code: Fettches the cde from the project repo
   4.  Install Front-end dependancies: runs the ```npm run frontend:install``` script in root package.json to install client side dependencies.
   5.  Install API dependencies: runes the script to install backend dependencies
   6.  Front-End Build: builds the client-side application to a directory of `www`. This is te directory that is later deployed on the S3 bucket.
   7.  API build: build the API to a `www` folder, copies the backed `package.json` to that folder, and then creates `Archive.zip` containing the project files. This .zip folder is the one later deployed on Elastic Beanstalk.

#### 2. Deployment:
   
   1. Install Node.JS
   2. Install EB CLI: installs the elastic beanstalk CLI, needed for deployment of backend
   3. Install and setup AWS CLI: CircleCI installs and configures AWS CLI on the enviroment using the keys of my account through enviroment variables I passed to Circle CI.
   4. Deploy app: Sets up Elastic Beanstalk enviroment using `eb init`, Deploys the `udagram-api/www/Archive.zip` file to EB, deploys the `udagram-frontend/www` directory to the S3 bucket for static web hosting.
   