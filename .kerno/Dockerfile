FROM node:18 AS build-env
ADD . /app
WORKDIR /app
RUN \
  npm install && \
  npm run compile && \
  rm -rf node_modules && \
  npm install --omit-dev --ignore-scripts

FROM node:18-slim
RUN apt-get update && apt-get install -y --no-install-recommends curl && rm -rf /var/lib/apt/lists/*
COPY --from=build-env /app/build /app/build
COPY --from=build-env /app/node_modules /app/node_modules
WORKDIR /app
CMD ["node", "build/src/index.js"]
