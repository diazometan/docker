FROM ruby:2.5

RUN apt-get update -y && \
	apt-get upgrade -y && \
	apt-get install -y nodejs postgresql-client && \
	mkdir -p /opt/app

#The ONBUILD command adds the instruction to work
#until the img is used as base of another build

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD EXPOSE 3000

ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed

# How to build it?
# docker build -t ft-rails:on-build .

#Resource: https://bitbucket.org/railstutorial/sample_app_4th_ed.git
