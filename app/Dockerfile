FROM debian:wheezy

RUN apt-get update && \
    apt-get install -y -q \
      build-essential \
      python-dev \
      python-pip && \
    rm -rf /var/lib/apt/lists/*

RUN pip install flask uwsgi

# Create a directory to deploy application and static files
ENV APP_DIR /application
ENV STATIC_DIR /static
ENV LOG_DIR /log
RUN mkdir -p $APP_DIR $STATIC_DIR $LOG_DIR

VOLUME [$APP_DIR, $STATIC_DIR, $LOG_DIR]

# Copy application files and install requirements on build
COPY . $APP_DIR/
RUN pip install -r $APP_DIR/requirements.txt
#ONBUILD COPY . $APP_DIR/
#ONBUILD RUN pip install -r $APP_DIR/requirements.txt

EXPOSE 5000

CMD ["uwsgi", "--socket", "0.0.0.0:5000", "--wsgi-file", "/application/app.py", "--callable", "app", "--processes", "2", "--threads", "4", "--logto", "/log/uwsgi.log"]
