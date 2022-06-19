#Base image
FROM nginx:1.21-alpine

#Remove the default nginx config
#replace it with your own nginx file. the one you are going to create
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
