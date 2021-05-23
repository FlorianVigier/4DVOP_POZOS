FROM python:3.6-stretch

MAINTAINER FlorianVigier_AdrienGauthier_AudeGrantais <LaDreamTeam@supinfo.com>

RUN apt-get update -y && apt-get install python-dev python3-dev libsasl2-dev python-dev libldap2-dev libssl-dev -y
RUN pip install flask flask_httpauth flask_simpleldap python-dotenv

VOLUME ./data

COPY ./student_age.py .
COPY ./student_age.json /data/student_age.json

CMD [ "python", "./student_age.py" ]

EXPOSE 5005