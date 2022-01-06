FROM ruby:2.7.2

WORKDIR /app

RUN dpkg --add-architecture amd64
RUN dpkg --print-foreign-architectures

# Using Node.js v14.x(LTS)
RUN curl -fsSL https://deb.nodesource.com/setup_14.x | bash -

# Add packages
RUN apt-get update && apt-get install -y \
      git \
      nodejs \
      vim

# Add yarnpkg for assets:precompile
RUN npm install -g yarn


# 依存パッケージのインストール
COPY Gemfile Gemfile.lock /app/

COPY . /app

RUN yarn install
RUN bundle install
# RUN bundle exec rails webpacker:compile

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3010

# Start the main process.
CMD ["rails", "server", "-p", "3010", "-b", "0.0.0.0"]

