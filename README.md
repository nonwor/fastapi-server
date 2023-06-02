# Course-Vector
The purpose of this repo is the document the local deployment of the FastAPI server running the ml model. There are many ways to do this, but we will wrap our FastAPI in a docker container and deploy it to Heroku. 

The app folder contains everything you need to run the FastAPI server locally with Unicorn server app. In the root folder, you will need Dockerfile, requirements.txt, and heroku.yml file.

## Local Docker Container
Make sure you have the Docker Engine installed. Make sure it is running the Linux container. This is because we will be building a Linux image to run the Python 3.9 environment as well as other Python packages. Why a Linux container? Because it is lightweight and stable.

If you are porting a Python notebook to FastAPI, all the !pip install will be ported over to requirements.txt as a plain text name.

```
docker build -t app-name .
docker run -p 80:80 app-name
```

Use this to test the FastAPI before deploying to Heroku. Once you are happy with the changes, do a git commit on the main branch. We will use git to push this code to Heroku. 

## Deploying Docker To Heroku
Download Heroku CLI and push the local code to a Heroku app/project

```
heroku login
heroku create app-name
heroku git:remote app-name
heroku stack:set container //this is to tell heroku that you will run docker container.
git push heroku main
```

Helpful Heroku functions:
Note: this should be run inside of the project. 
```
heroku -logs --tail //show latest log
heroku ps:scale web=0 //this is to "turn off" the machine
heroku ps:scale web=1 //this is to assign 1 web worker server
```


