# flask-uwsgi-nginx

Build and run app image :

    $ cd app
    $ sudo docker build -t="matthieubosquet/flask-uwsgi" .
    $ sudo docker run -d -P -v $(pwd)/log:/log -v $(pwd)/static:/static --name app matthieubosquet/flask-uwsgi

Build and run nginx image :

    $ cd ../nginx
    $ sudo docker build -t="matthieubosquet/uwsgi-nginx" .
    $ sudo docker run -d -p 5000:80 --name nginx --link app:app --volumes-from app:ro matthieubosquet/uwsgi-nginx
