FROM python:3.10

RUN mkdir -p /home/webapp
WORKDIR /home/webapp
COPY . /home/webapp
RUN pip install -r requirements.freeze
CMD [ "flask", "run", "-p", "8080" ]
