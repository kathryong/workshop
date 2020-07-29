# the environment
FROM node:14
 
ENV APP_DIR=/appAPP_PORT=3000
 
WORKDIR ${APP_DIR}
 
ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views
 
RUN npm install

#Add healthcheck 
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
        CMD curl -s -f http://localhost:${APP_PORT}/health || exit

EXPOSE ${APP_PORT}
 
ENTRYPOINT ["node","main.js"]

