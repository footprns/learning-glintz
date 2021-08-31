FROM python:3.9-alpine

LABEL version="1.0"
LABEL app="flask"

WORKDIR /usr/src
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
# CMD [ "ls" ]
# CMD [ "ls", "-la", "/usr/src" ]
