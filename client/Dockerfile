FROM node:alpine as builder

WORKDIR '/app'

COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

# use base image
FROM nginx
# what network port to listen
EXPOSE 3000
# overwrite default nginx config file with our oun
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# from the result of the 'builder' phase 
# take the contents of the '/app/build' folder and put it in the '/usr/share/nginx/html' folder
COPY --from=builder /app/build /usr/share/nginx/html