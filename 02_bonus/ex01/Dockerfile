#NodeJS + npm + yarn

FROM ubuntu

RUN apt-get update && apt-get upgrade -y \
	&& apt-get install -y nodejs npm git vim

RUN npm install yarn --global && npm install npm --global

# How to build it?
# docker build -t ex01 .

# How to run it?
# docker run --rm -ti ex01
