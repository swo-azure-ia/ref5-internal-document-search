# Stage 1: Compile and Build FE
FROM node:17-alpine as FE_Builder
WORKDIR /usr/local/app

# Add the source code to app
COPY . /usr/local/app/

# Install all the dependencies
RUN npm --prefix ./frontend install ./frontend

# Generate the build of the application
RUN npm --prefix ./frontend run build

# Stage2: Build BE
FROM ubuntu:latest

ENV FLASK_APP="backend/app.py"

RUN apt update
RUN apt install python3 python3-pip curl -y

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

RUN mkdir /backend

COPY --from=FE_Builder /usr/local/app/backend /backend

RUN pip3 install -r /backend/requirements.txt

EXPOSE 5000
CMD [ "flask", "run","--host","0.0.0.0","--port","5000"]