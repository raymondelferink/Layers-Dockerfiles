FROM learninglayers/base

MAINTAINER Petru Nicolaescu

# install mysql client
RUN apt-get -y install mysql-client

RUN apt-get install -y wget \
					tar \
					unzip \
					 mysql-client \
					 openjdk-7-jre \
					 dos2unix
					 
WORKDIR /opt
			
RUN  wget http://mirror.arcor-online.net/www.apache.org/tomcat/tomcat-7/v7.0.59/bin/apache-tomcat-7.0.59.tar.gz && \
	 mkdir /opt/tempdircopy && \
	 mkdir /opt/tomcat && \
	 tar -zxvf /opt/apache-tomcat-7.0.59.tar.gz -C /opt/tempdircopy && \
	 cp -r /opt/tempdircopy/apache-tomcat-7.0.59/* /opt/tomcat && \
	 rm -r /opt/tempdircopy && \
	 wget http://layers.dbis.rwth-aachen.de/jenkins/job/OpenIDConnect%20Server/lastSuccessfulBuild/artifact/*zip*/target.zip && \
	 unzip target.zip && \
	 mv /opt/archive/openidconnectldapoverlay/ldap-server-overlay/target/o#oauth2.war /opt/tomcat/webapps/o#oauth2.war
	     
CMD	 echo "The MYSQL pass is $OIDC_MYSQL_PASSWORD and $OIDC_MYSQL_USER" && \
	 mysql -u$OIDC_MYSQL_USER -p$OIDC_MYSQL_PASSWORD -hmysql OpenIDConnect < /etc/sql/schema.sql && \
	 dos2unix /opt/tomcat/bin/startup.sh && \
	 chmod +x /opt/tomcat/bin/startup.sh && \
	 /opt/tomcat/bin/catalina.sh run

EXPOSE 8080
