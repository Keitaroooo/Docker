FROM ruby:2.6.5

RUN apt update -qq && \
apt install -y build-essential \
libpq-dev \
nodejs
    
RUN mkdir /app
ENV APP_ROOT /app
WORKDIR $APP_ROOT
# このファイル（Dockerfile）と同じ階層にあるGemfile等をコンテナにコピー
COPY ./Gemfile $APP_ROOT/Gemfile
COPY ./Gemfile.lock $APP_ROOT/Gemfile.lock
# コンテナのGemfileを参考にGemをインストール
RUN bundle install
# このファイルが含まれているディレクトリをコンテナのルートディレクトリにコピー
COPY . $APP_ROOT

COPY ./entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 8000

CMD ["rails", "server", "-b", "0.0.0.0"]
