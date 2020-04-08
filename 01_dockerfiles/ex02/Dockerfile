FROM ruby

RUN gem install rails && apt update && apt install nodejs -y && apt autoclean

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install && rake db:migrate && rake db:seed
