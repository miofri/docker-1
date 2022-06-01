# --BEFORE STARTING--
# create a rail app -> rails new app
# test that it works -> localhost:3000

FROM ruby:3.0

# -qq No output except for errors
RUN apt-get update -qq && apt-get install -y nodejs sqlite3 npm build-essential libpq-dev yarn

# The ONBUILD instruction adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build. The trigger will be executed in the context of the downstream build, as if it had been inserted immediately after the FROM instruction in the downstream Dockerfile.
# ONBUILD RUN gem install bundler
# ONBUILD RUN gem install sqlite3
# ONBUILD RUN gem isntall yarn

ONBUILD WORKDIR /opt/app/
ONBUILD COPY ./app /opt/app
ONBUILD RUN gem install rails
ONBUILD RUN bundle install
ONBUILD RUN bundle update --bundler

# ONBUILD RUN npm install --global yarn
# rake is ruby's task runner.
ONBUILD RUN rake db:create
ONBUILD RUN rake db:migrate

# Delete Gemfile.lock and make sure ruby version is ruby '3.0.4' and 'rails', '~> 7.0.0'

# docker build -t ft-rails:on-build .

# docker build -t subject -f subject_school .

# docker run -it -p 3000:3000 --rm subject
