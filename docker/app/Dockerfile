FROM ruby:2.5.1

MAINTAINER dilkhushsoni2010@gmail.com

ENV BUNDLER_VERSION=2.0.2

ENV RAILS_ROOT /var/www/rails-docker

RUN mkdir -p $RAILS_ROOT

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

RUN apt-get update && apt-get install -y \
      binutils-gold \
      build-essential \
      curl \
      file \
      g++ \
      gcc \
      git \
      less \
      libstdc++ \
      libffi-dev \
      libc-dev \
      libxml2-dev \
      libxslt-dev \
      libgcrypt-dev \
      make \
      netcat-openbsd \
      nodejs \
      openssl \
      python \
      tzdata


RUN gem install bundler -v 2.0.2

WORKDIR $RAILS_ROOT

ENV RAILS_ENV='development'
ENV RACK_ENV='development'

COPY Gemfile Gemfile.lock ./

RUN bundle config build.nokogiri --use-system-libraries

RUN bundle check || bundle install

#CMD ["export", "SECRET_KEY_BASE='bin/rake secret'"]

COPY yarn.lock package.json ./

RUN npm --version

RUN npm install -g yarn

RUN yarn install --check-files

COPY . ./

#RUN bundle exec rake assets:precompile SECRET_KEY_BASE=$SECRET_KEY_BASE

EXPOSE 3000

CMD ["bundle", "exec", "puma", "-C", "config/puma.rb"]
