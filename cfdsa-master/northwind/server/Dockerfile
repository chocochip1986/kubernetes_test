##Building....
#Base Image
FROM node:latest

ENV DB_HOST=db_container DB_PORT=3306 \
    DB_USER=root DB_PASSWORD=changeit \
    APP_DIR=/app APP_PORT=5000

WORKDIR ${APP_DIR}

ADD main.js .
ADD package.json .
ADD public public
ADD views views
ADD config config

RUN npm install

##Running...
EXPOSE ${APP_PORT}

HEALTHCHECK --interval=60s --timeout=30s --retries=3 \
	CMD curl -f -s http://localhost:${APP_PORT}/health || exit 1

ENTRYPOINT ["node", "main.js"]