FROM ubuntu:19.10

MAINTAINER max-30ru@mail.ru
run apt-get update -y && \
       apt-get install -y python3-pip \
                          git \
                          libpcre3 \
                          libpcre3-dev \
                          libpq-dev && \
       apt-get -y autoremove && \
       apt-get -y clean && \
       rm -rf /var/lib/apt/lists/*


WORKDIR /srv/app

run git clone https://github.com/mbaran0v/python-sample-app.git /srv/app
run pip3 install -r requirements.txt && \
                    pip3 install uwsgi && \
                    pip3 install supervisor && \
                 rm -rf /root/.cache

COPY conf/supervisord.conf /etc/supervisord.conf
COPY conf/uwsgi.ini /etc/uwsgi/wsgi.ini
# устраняем костыль
#ModuleNotFoundError: No module named 'wsgi'
#flask_app_1  | unable to load app 0 (mountpoint='') (callable not found or import error)
#flask_app_1  | unable to find "application" callable in file app.py
#flask_app_1  | unable to load app 0 (mountpoint='') (callable not found or import error)
# описание https://stackoverflow.com/questions/12030809/flask-and-uwsgi-unable-to-load-app-0-mountpoint-callable-not-found-or-im

COPY conf/application.py /srv/app/application.py

CMD flask db upgrade

EXPOSE 5000
