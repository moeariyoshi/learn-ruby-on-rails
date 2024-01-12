##########################
## Builder Container
##########################
FROM ruby:3.2.1-alpine3.17 as builder

WORKDIR /learn-ror

RUN apk update && \
    apk add --no-cache \
      # Essential build tools like compilers and make.
      build-base \ 
      # Development files for XML and XSLT support.
      libxml2-dev \
      libxslt-dev \
      # Header files needed for building certain software.
      linux-headers \
      # PostgreSQL client library.
      libpq \
      mysql-dev \
      # MIME database used by various applications.
      shared-mime-info && \
    gem install bundler

COPY Gemfile Gemfile.lock ./

RUN bundle config set --global force_ruby_platform true && \
    bundle install

##########################
## Application Container
##########################
FROM ruby:3.2.1-alpine3.17

WORKDIR /learn-ror

RUN apk update && \
    apk add --no-cache \
      build-base \
      # Development files for the cURL library.
      curl-dev \
      libxml2-dev \
      libxslt-dev \
      # Header files needed for building certain software.
      linux-headers \
      libpq \
      # MySQL client and development files.
      mysql-client \
      mysql-dev \
      less \
      nodejs \
      tzdata \
      git && \
    gem install bundler && \
    bundle config set --global force_ruby_platform true

COPY --from=builder /usr/local/bundle /usr/local/bundle
COPY . .
