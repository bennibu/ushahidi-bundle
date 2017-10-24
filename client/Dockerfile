FROM node:6.11.4-stretch

RUN apt-get update && \
  apt-get install --no-install-recommends --no-install-suggests -y \
    nginx-light && \
  rm -rf /var/lib/apt/lists/* && \
  ln -sf /dev/stdout /var/log/nginx/access.log && \
	ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx-site.conf /etc/nginx/sites-available/default

ENV VERSION v3.7.1
RUN git clone https://github.com/ushahidi/platform-client \
      /tmp/client && \
  cd /tmp/client && \
  git checkout tags/$VERSION && \
  git checkout -b deploy 


ENV BACKEND_URL="{{backend_url}}"
RUN cd /tmp/client && \
  npm install && \
  npm install gulp && \
  node_modules/gulp/bin/gulp.js build && \
  rm -r /var/www/* && \
  mv /tmp/client/server/www /var && \
  npm cache clean && \
  rm -rf /tmp/*


COPY start.sh /

EXPOSE 80

CMD ["/start.sh"]
