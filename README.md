# my-docker-lab
Having fun with docker by building and exploring the wonderful world of containerization

Learning us a beginner
1st project: Containerizing my simple node express app

- Dependencies I had to install on my local machine
- Npm install
- npm i express
- npm i dotenv
- npm i nodemon --save-dev
  
What I did?
- Wrote a simple index.js express app code with a running server
- Wrote my Dockerfile which would be used as an image
- In my Dockerfile, I set the base image, the working directory, copied my package.json file into my would be container path
- I run some dependencies eg. npm install
- copied all the files on the pwd of my local machine to the /app path of my would be container
- Exposed my port
- then CMD npm run dev

Configuration in my package.json
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon -L index.js"
  }"

First approach with containerizing my express app
- I built the image from the Dockerfile by running this command : docker build -t myapp-image
- I gave the image a tag of "myapp-image"
- I then run the myapp-image as a container by using this command: docker run -v ${pwd}:/app -v /app/node_modules -p 4000:4000 -d --name myapp-container myapp-image

- Done the app was containerized and I was able to run my web server on my local machine from the container

Second Approach
Build a docker-compose.yml
Here is the code

version: "3"
services:
  myapp-container:
    build: .
    ports: 
      - "4000:4000"
    volumes: 
      - ./:/app
      - /app/node_modules

run this command to build the image through the dockerfile and run the image as a container from the docker-compose.yml: docker-compose up -d 
to delete the container use this command : docker-compose down
