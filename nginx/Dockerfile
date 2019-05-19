FROM nginx:alpine

# create public directory
RUN mkdir /home/mizzsig && \
    mkdir /home/mizzsig/sssignal2-2 && \
    mkdir /home/mizzsig/sssignal2-2/public

# remove default conf
RUN rm /etc/nginx/conf.d/default.conf

# set sssignal conf
COPY nginx /etc/nginx

# set Japanese time
RUN apk --update add tzdata
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN apk del tzdata
RUN rm -rf /var/cache/apk/*