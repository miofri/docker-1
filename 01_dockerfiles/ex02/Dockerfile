# Your generic container should install, via a ruby container, all the necessary dependencies and gems, then copy your rails application in the /opt/app folder of your container. Docker has to install the approtiate gems when it builds, but also launch the migrations and the db population for your application. The child Dockerfile should launch the rails server (see example below).
# we are creating an image

FROM ruby:3.0

RUN apt-get update -qq && apt-get install -y nodejs sqlite3

# The ONBUILD instruction adds to the image a trigger instruction to be executed at a later time, when the image is used as the base for another build. The trigger will be executed in the context of the downstream build, as if it had been inserted immediately after the FROM instruction in the downstream Dockerfile.

ONBUILD COPY app /opt/app
ONBUILD WORKDIR /opt/app

ONBUILD RUN gem install bundler
ONBUILD RUN bundle install
ONBUILD RUN rails db:create
ONBUILD RUN rails db:migrate