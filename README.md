# devops_blog
an introduction to django using the buildout of a blog site

You can clone this project or you can use your own project, the idea is to follow the steps listed in this README to deploy your project or any other django project to docker. 
That being said, listed below are the steps that were used to make this work. 
Remember to dump the database before you start. 
- At the root of your application where you have the manage.py file, run:
  - python manage.py dumpdata >> data.json. This assumes that your virtual environment is active. Also you can call the dump file anythig you want. 
1. Comment out the run command from the docker file. This should be in the application
2. Create the docker-compose file at the root of the project outside of the application 
3. Edit the settings.py file, add the entry for the secret key, debug and allowed_hosts. i.e you are telling the settings.py file to get those settings from the environment varibales. This assumes that you have a .env file at the root of the project. 
4. Build with docker-compose build 
5. Run with docker-compose up -d 
6. Validate that its working
7. Add the info for the db to the .env file. Look at the .env file in this project to see what I am talking about. 
8. Edit the settings.py file again and add the database info. Again, look at the settings.py file for this project. 
9. Add the info for the db to the docker-compose file. 
10. Add psycopg2-binary to the requirements file if its not already there. 
11. Build the new images with docker-compose up -d --build
12. Run the migrations with: docker-compose exec web python manage.py migrate --noinput
13. Run the shell with: docker-compose exec web python manage.py shell
14. Run these two lines one at a time: "from django.contrib.contenttypes.models import ContentType", "ContentType.objects.all().delete()"
15. now load the data from the json file that we dumped earlier. run "python manage.py loaddata data.json"
16. Add gunicorn to the requirements.txt file if its not already there.
17. Create a folder for nginx at the root of your project. This should be at the same level as your docker-compose.yml file. create two files in that folder: Dockerfile and nginx.conf
18. Add the config for nginx to the docker-conpose file
19. Add the nginx config to the Dockerfile in the nginx directory … also add the nginx config to the nginx.conf file
20. Change the port for the web app to Expose. In the docker-compose file this has already been done.  
21. Run it again … you should be able to access the app on port 1337 now 
22. Now if you try to access the admin of this site you will notice that it has no formatting … so lets fix that 
23. Add the config for static files to the settings.py file
24. Add volumes for the static files to web and nginx sections of the docker compose file
25. Add the alias for the nginx config … 
26. Run the build again … 
27. That is it … now there a few things that you do additionally but because our app is not complete you can google it when you get to that 

