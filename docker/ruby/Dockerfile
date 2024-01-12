##########################
## Builder Container
##########################
FROM ruby:3.2.1-alpine3.17 as builder

WORKDIR /learn-ror

RUN gem install bundler

COPY Gemfile Gemfile.lock ./

RUN bundle config set --global force_ruby_platform true && \
    bundle install

##########################
## Application Container
##########################
FROM ruby:3.2.1-alpine3.17

WORKDIR /learn-ror

RUN gem install bundler && \
    bundle config set --global force_ruby_platform true

COPY --from=builder /usr/local/bundle /usr/local/bundle
COPY . .
