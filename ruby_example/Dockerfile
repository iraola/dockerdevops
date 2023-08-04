FROM ruby:3.1.0

EXPOSE 3000

WORKDIR /usr/src/app

# Install the correct bundler version
RUN gem install bundler:2.3.3

# Trick: copy files for required dependencies to be installed
COPY Gemfile* ./

# Install dependencies
RUN bundle install

# Copy project
COPY . . 

RUN rails db:migrate RAILS_ENV=production
RUN rake assets:precompile

CMD ["rails", "s", "-e", "production"]
