# flask-uwsgi-nginx

To get containers running :

sudo docker build -t="matthieubosquet/flask-uwsgi" app

sudo docker build -t="matthieubosquet/uwsgi-nginx" nginx

 sudo docker run -d -P -v $(pwd)/app/log:/log -v $(pwd)/static:/static --name app matthieubosquet/flask-uwsgi

 sudo docker run -d -p 5000:80 --name nginx --link app:app --volumes-from app:ro matthieubosquet/uwsgi-nginx
