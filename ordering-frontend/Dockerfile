FROM node:20

WORKDIR /app

# COPY public public
# COPY src src
# COPY .env .
# COPY babel.config.js .
# COPY jsconfig.json .
# COPY package-lock.json .
# COPY package.json .
# COPY vue.config.js .
# docker ignore 사용하면 전체를 복사해도 불필요한 파일은 제외하고 빌드 가능
COPY . . 

RUN npm install

ENTRYPOINT [ "npm", "run", "serve" ]