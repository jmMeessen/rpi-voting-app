FROM hypriot/rpi-node:slim

WORKDIR /app

ADD package.json /app/package.json
RUN npm install \
	&& npm ls \
	&& mv /app/node_modules /node_modules

ADD . /app

ENV PORT 80
EXPOSE 80

CMD ["node", "server.js"]
