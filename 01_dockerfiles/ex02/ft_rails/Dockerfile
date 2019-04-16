FROM    ruby:2.3.1

RUN     apt-get update
RUN     apt-get install -y sqlite3
RUN		apt-get install -y nodejs
RUN     gem install rails
RUN     gem install sqlite3

ONBUILD ADD     ["app", "/opt/app"]
ONBUILD WORKDIR /opt/app

ONBUILD RUN     bundle update && bundle install && rake db:migrate && rake db:seed
