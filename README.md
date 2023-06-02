# Course-Vector
The purpose of this repo is the document the local and the deployment of the FastAPI server runing the ml model. There are many way to do this, but we will wrap our FastAPI in a docker container and deploy to heroku. 

The app folder contains everything you need to run the FastAPI server locally with Unicorn server app. In the root folder, you will need Dockerfile, requirements.txt, and heroku.yml file.

## Local Docker Container
Make sure you have the Docker Engine installed. Make sure it is running the linux container. This is because we will be build a linux image to run the python 3.9 environemnt as well as other python packages. Why a linux container? Becasue it is lightweight and stable.

If you are porting a python notebook to FastAPI, all the !pip install will be port over to requirements.txt as plain text name.

```
docker build -t app-name .
docker run -p 80:80 app-name
```

Use this to test the FastAPI before deploying to heroku.
Once you are happy with the changes, do a git commit on main branch. We will use git to push this code to heroku. 

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


