FROM footprns/flask:0.1

LABEL version="2.0"
LABEL app="flask"

WORKDIR /usr/src
COPY . .

# ENV FLASK_APP=hello.py
EXPOSE 5000/tcp
CMD [ "flask", "run", "--host=0.0.0.0" ]
# CMD [ "ls", "-la", "/usr/src" ]