FROM node:18 AS build
WORKDIR /app

# copy package.json and lock file first
COPY package*.json ./

# install but skip optional deps (skips native rollup binding)
RUN npm install --legacy-peer-deps --no-optional

# copy rest of code
COPY . .

# ensure rollup is rebuilt as JS fallback
RUN npm install rollup@^4 --force

# build project
RUN npm run build


FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
