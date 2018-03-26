FROM        ubuntu:14.04.2
MAINTAINER  Love Nyberg "love.nyberg@lovemusic.se"
ENV REFRESHED_AT 2014-10-18

# Update the package repository and install applications
RUN apt-get update -qq && \
  apt-get upgrade -yqq && \
  apt-get -yqq install varnish && \
  apt-get -yqq clean

# Make our custom VCLs available on the container
ADD varnish/varnish.service /lib/systemd/system/varnish.service
ENV VARNISH_PORT 80

# Expose port 80
EXPOSE 80

# Expose volumes to be able to use data containers
#VOLUMES ["/var/lib/varnish", "/etc/varnish"]

ADD varnish/start.sh /start.sh
CMD ["/start.sh"]
