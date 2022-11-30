FROM node:10-slim as prod
EXPOSE 3000
ENV NODE_ENV=production
WORKDIR /app
COPY package*.json ./
# --only=production for node:10
# --production for newer node version (2022)
RUN npm install --only=production \
    && npm cache clean --force
COPY . .
CMD ["node", "./bin/www"]

FROM prod as dev
ENV NODE_ENV=development
# --only=development for node:10
# --development for newer node version (2022)
RUN npm install --only=development
CMD ["node_modules/nodemon/bin/nodemon.js", "./bin/www", "--inspect=0.0.0.0:9229"]

FROM dev as test
ENV NODE_ENV=development
# RUN npm run test
CMD ["npm", "test"]
