FROM learninglayers/base

MAINTAINER Dominik Renzel

# install mysql client
RUN apt-get -y install mysql-client

# Install build tools
RUN apt-get install -y \
                     wget \
                     unzip \
					 mysql-client \
                     openjdk-7-jre \
                     dos2unix

RUN mkdir /opt/mobsos-monitor
RUN mkdir /opt/mobsos-monitor/etc
WORKDIR /opt

# Download and unzip newest build from CI server, prepare database connections and then start. 
CMD wget http://layers.dbis.rwth-aachen.de/jenkins/job/MobSOS%20Monitor/lastSuccessfulBuild/artifact/*zip*/archive.zip && \
    unzip archive.zip && \
	rm -rf archive/etc && \
	cp -R archive/* mobsos-monitor && \
	rm -rf archive.zip archive && \
    cd mobsos-monitor && \
	mysql -uroot -p$MYSQL_ROOT_PASSWORD -hmysql < etc/sql/schema.sql && \
	dos2unix bin/start.sh && \
    chmod +x bin/start.sh && \
    bin/start.sh /usr/local/openresty/logs/access.log

